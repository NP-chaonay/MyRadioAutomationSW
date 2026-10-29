# NP-chaonay's version of Radio Automation Software

# DRAFTING ZONE
NP-chaonay's version of Radio Automation created by Python. Designed to be modular and customizable; Fail-safe mechanism existed; and also, is lightweight.

Inspired by: [EVENT] Songs is playing via School PA in morning before assembly meetup.

## Module List
- Main: Central/shared's API (such as Logging ... place for variable for instance of each module ) + Auto Fatal Recovery (such as auto-restart module)
- Scheduling: Interpret config section "Scheduling" and follow it... and take action specified in schedule (issue command/param to module "Player Orchestration").
- Player Orchestration: Managing each instance of Music Player Control... act as broker for Scheduling module to command about module "Song Selection" and "Music Player Control"
- Song Selection: Module that do logic what next song will be playing
- Music Player Control: Module that control external Music Player (or even radio streaming instead of playing // or playing microphone sound) 
- Remote Control: Module that allow control the system from such as HTTP Console / socket file

## Example of feature supported
- Specify how to do when old entry is expired due to "Expired Time" or new-entry's time is arrived (can set entry not to be expired when new-entry time is arrived)... and maximum of active entry simultaneously
- recovery stuff such as
  - Main Module: Restart related (i dont yet think what module should be restarted which depend on what module is failed) module if fatal happen on any module... and soft restart is not possible (if supported by that module)
  - Soft Restart method: This try to keep current state (such scheduling ... what song is playing and what time position of song ... state of random of song selection module)  as much as possible... required implementation of each module to have soft-restart implmenetation.
  - Resume method: same as above but no error-handling-stuff code... use in case such as when the system's computer is power loss
- Playlist Weighting and shuffle-instead-of-pure-random and so-on that radio automation support
- In Config File, config parts are separated by module... setting scheduling is also set in config file.
- Music Player Control support mpv (using --config=no by default)
- Player Orchestration support such as: mute/duck/pause/stop bg-music stream and higher prioirty stream is playing (so Player Orchestration can support flag what type of stream + and priority value (per-stream and per-type-of-stream)
- logging tell what module make that log + datetime
- for scheduling support various schedule type... action for a entry specified in schedule
- support "channel" where "Player Orchestration" get value of channel and pass to "Music Player Control" and "Song Selection"... this can make this single Radio Automation system able to do 2+ stream/play simultaneously and separately... "Player Orchestration" of any channel of will not interfere of another channel...
- in case of more custom there is API of each module that let each module to use
- so if someone want to modify some module... just edit code or replace code of that module by the one you want.... the code of module is in OOP... so you can just define inheritant class... want to add another type of module? you can... (useful when Main module want to do auto-restart in fatal eror)
