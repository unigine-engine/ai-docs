# Running Tracks in Application


After the track-based animations were created in UnigineEditor, they need to be played in the application. To add this functionality to your project:


1. In the Asset Browser, right-click and select *Create Code > USC*.
2. Open the created file in your IDE and replace its contents with the following code: ```cpp #include <core/systems/tracker/tracker.h> Unigine::Tracker::TrackerTrack track; float time, min_time, max_time, unit_time; int init() { // use the Tracker namespace using Unigine::Tracker; // create a Tracker instance that will play the tracks Tracker tracker = new Tracker(); ${#HL}$	// load the required tracks from a file track = tracker.loadTrack("samples/tracker/tracks/render_00.track");${HL#}$ // get the start time of the track (in units) min_time = track.getMinTime(); // get the end time of the track (in units) max_time = track.getMaxTime(); // get the duration of the track unit (in seconds) unit_time = track.getUnitTime(); // set the initial time to play the tracks time = track.getMinTime(); return 1; } int update() { if(track == NULL) return 1; // update the tracks animation time time += engine.game.getIFps() / unit_time; time = min_time + ((time - min_time)) % (max_time - min_time); // set animation time for tracks (time values outside the [mintime, maxtime] range are clamped automatically) if(engine.game.isEnabled()) track.set(time); return 1; } ``` > **Notice:** Time values outside the [**MinTime, MaxTime**] range are clamped automatically.
3. Update the path to your `.track` file (located in the `/data` folder), save the script and return to the Editor.
4. Select your `.world` file and drag the created `.usc` file into the *Script* field in the *Parameters* tab. ![](track_script.png)
5. Save and run the project.
