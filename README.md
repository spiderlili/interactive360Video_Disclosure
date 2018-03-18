# interactive360Video_Disclosure

How To Use:

main menu scene:
A test bed to run directly in the editor without a vr headset.
It has a directional light and a camera with a camera editor control script on it to emulate head movement using a mouse. turn this off for now. hover over any of the buttons to load a new scene which will contain a 360 video. hit pause to pause the video and hit play to play the video again

mainMenuManager object:
has a menu manager script on it
a fadeout ui object to handle fading between scenes
an eventsystem which handles the input
a video manager game object with a gameManager script on it - handles the loading of the scenes from the main menu.

mainMenuEditor object:
contains the interactive UI, with a menuManager script which manages the buttons and allows them to load the next scene.
it also toggles between the pause and the play button. the occulus menu toggle will not be used when testing the editor.
3 elements for the buttons in scene - option 1 - 3 which corresponds to the 3 elements on the videoManager object which specifies the scenes to load.

The video scenes are in the videoscene folder.
the videoplayer component is playing back the video onto the unity skybox. source of the videoplayer component is using the 360 video.

2D Video scene:
set up the video to play on awake and waiting for the first frame
the render mode is very important: playing this to render a texture
the target texture is specified as 3D_3840x2160 = a common pixel size for 360 videos. This must match the exact size of the video(check file's source info) = 2200 x 1100

The rendertextures folder contains sample textures for common 360 sizes.
to create your own render texture: create > render texture > specify the size to match the size of the video
need to map the render texture to the skybox of the scene: window > lighting > settings - assign the appropriate skybox with the right size

Create a custom skybox for the 360 video:
use the skybox/paranomic shader which is essential for playing the video on a skybox
mapping = lattitude longtitude layout
image type = 360 degrees(can also do 180 degree videos)
Don't have a 3d layout when using a 2d video

3D Video scene:
must wear the headset to see the 3D elements because the skybox material set up is different in 3D compared to 2D using a different target texture. in windows lighting: the skybox material is different
change skybox 3D layout option to over under because the video is using the over under layout.

Main menu gaze scene:
similar to main menu scene but uses gaze-based interactions
make sure VR toggle is VR enabled at the top menu
the green dot is where the gaze is - the gaze triggers the loading of the next scene
main menu ui is different
main menu gaze prefab
main menu manager
on main menu gaze: rendering this canvas in world space - for VR always render things in the world space. otherwise it's going to be a very unpleasant experience for the user.
important to make sure the interactable parameter in the selection slider under the main menu gaze > control ui > selection slider is matched up to the correct option.

the VR eye raycaster script chooses a raycast and detect if it's come into contact with any interactable game objects.
VR camera UI renders the small green dot that the user sees when they're looking.

Hotspot example gaze scene:
can be used for any vr headset. instead of having a main menu style of interaction, interact with the scene using hotspots.
hotspot represented by feet icon: if coming into contact with it, then it will trigger a new scene to run in the same location.

hotspot manager contains all of the hotspots in the scene:
under the hotspot game object: organise different hotspots
make sure to place the hotspot close to the camera and overlays well against the video backdrop.
attach the hotspot button gaze script on the hotspot which triggers the selection image to start filling when the user's gaze has been in contact with the hotspot.

Main menu controller scene:
Adds interactivity with the oculus touch controllers.
Use the index trigger to trigger the next scene to load.
can enjoy the video and use buttons to trigger the menu instead of having the menu on your face
the player game object contains a camera, RH(right hand), LH(Left Hand)
get tracking information from the oculus touch controllers using the tracked pose driver script. set them up separately for each hand.
on the RightControllerPF object: shoot out a raycast input to detect if the raycast coming out of the hand has come into contact with any interactable objects.
Oculus primary input axis: specifies which button the oculus touch controller to trigger the raycast(SecondaryIndexTrigger = the right hand)

on the main menu manager object: set up oculus menu toggle to button 2(B button on the right controller)

MainMenu_GVR_Controller Scene:
The google VR controller scene which integrates the Google VR SDK to get input from the daydream view controller and add interaction. Switch the build settings to Android.

The player object contains the main camera and google VR controller prefabs
GVRInstantPreviewMain allows for instant testing without a headset.

Notes:
Need to create an audio source for the audio on the video player(set audio output mode to audio source)

