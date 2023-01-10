# How messages are built from seed files
* `klist_t(lms)` ~= linked list
* `KLIST_INIT(lms, message_t *, message_t_freer)` -> initialize datastructure (linked list) of `message_t` and utilities functions
* `klist_t(lms) *construct_kl_messages(u8* fname, region_t *regions, u32 region_count)` -> build a linked list of `message_t` from a seed in the file `fname` and a *description of regions*
    - a region is a portion of a message correponding to one send/receive
    - the function `region_t* extract_requests_generic(unsigned char* buf, unsigned int buf_size, unsigned int* region_count_ref)` builds the regions from a seed (used in function `static void add_to_queue(u8* fname, u32 len, u8 passed_det)` -> in fact `extract_requests` which is equal to `extract_requests_generic`)

# How does the forkserver works
* Instead of cloning the whole SUT for each new fork, the cloning is done within the binary of the SUT: code is injected into the fuzzed binary.
* [https://lcamtuf.blogspot.com/2014/10/fuzzing-binaries-without-execve.html](https://lcamtuf.blogspot.com/2014/10/fuzzing-binaries-without-execve.html)
* In `afl-fuzz.c:init_forkserver` and in `afl-as.h` and `afl-as.c` (instrumentation added in assembly language)
* StateAFL has two forkservers available depending if stateAFL probes are used or if *vanilla* binary is used instead (option `-u`)

# The function `choose_target_state`
* choose a state within all the states discovered so far
* take a selection algorithm in arguments
* select an id (`target_state_id`) corresponding to a state in the hash map `khms_states`
* `khms_states` is a hash map of struct `state_info_t`

# The function `choose_seed`
* produce a `queue_entry` from a state selected
* take a selection algorithm in arguments
* A `queue_entry` contains a seed, the regions decomposition and the state
* A region contains the state sequence produced until the end of the region

# The function `update_scores_and_select_next_state`
