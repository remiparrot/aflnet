# Advice from AFLNet's README
- [x] Look at the function `choose_target_state`
- [x] Look at the function `choose_seed`
- [ ] Look at the function `update_scores_and_select_next_state`

# ~Remove the probes (on memory allocation and on network communication) added at compilation on memory~
- [/] ~reset folder llvm\_mode as in aflnet project~

# Don't care about the messages sent by the SUT
* In `int main(int argc, char** argv)`:
    - [x] remove target protocol selection (see StateAFL)

# Remove the state machine building process
* Disable option `-E` disable the state machine building and selection of state to fuzz
    - [ ] follow the boolean variable `state_aware_mode`
* In `int main(int argc, char** argv)`:
    - [/] ~remove `check_aslr()` call~
* In `int setup_ipsm()`:
    - [x] only initialize the state hash map `khms_states`
* ~In `EXP_ST void setup_shm(void)`:~
    - [/] ~(?) remove state related stuff: TLSH calibration, log state tracer, .. -> this is somehow related to the forkserver~
* In `EXP_ST void setup_dirs_fds(void)`:
    - [ ] remove records of new paths
* In `EXP_ST u8 common_fuzz_stuff(char** argv, u8* out_buf, u32 len)`:
    - [ ] remove the AFLNet update of `kl_messages` linked list
    - [ ] remove `update_fuzzs()` call

# Build a very simple state list from the seeds files
* In `static void perform_dry_run(char** argv)`:
    - [ ] build message from *replay* format (see StateAFL)
* In `void update_state_aware_variables(struct queue_entry *q, u8 dry_run)`
    - [ ] build a simple state list only if it is a *dry run*
    - [ ] otherwise do nothing
* The hash map `khms_states` should be this list
    - [ ] initialize it in `update_state_aware_variables` in *dry run* mode
    - [ ] never update it after the initialisation
* The type `region_t` should not contain state related stuff (in file `aflnet.h`)

# Select the messages to mutate directly from the seeds files
* In `struct queue_entry *choose_seed(u32 target_state_id, u8 mode)`
    - [ ] build a `queue_entry` from the seed file corresponding to the state given as argument
* In `static u8 fuzz_one(char** argv)` after the flag `AFLNET_REGIONS_SELECTION`
    - [ ] retrieve the M2 part of the messages from the file `length-seed.state[X]` instead of the region information


# Select the states in a round-robin fashion (or any other "fair" selection)
* In the function `choose_target_state`
    - [ ] add a new selection algorithm based on the simple state list

# Take a look at the mutation functions added in `static u8 fuzz_one(char** argv)` (in StateAFL)
- [ ] `void regions_add_bytes(region_t* regions, unsigned int region_count, unsigned int position, int added_bytes)`
- [ ] `int regions_remove_bytes(region_t* regions, unsigned int region_count, unsigned int position, int removed_bytes)`
- [?] static variables `unsigned int mutated_region_count` and `region_t* mutated_regions`
