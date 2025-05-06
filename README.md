# Escape-Hunt:Mixed-Reality (MR)
1. System Implementation
1.1 Build and Project Settings
To deploy the MR game correctly on Meta Quest 3, the Unity project requires specific configurations.
Step 1: Build Settings
•	Platform: Android
•	Texture Compression: ASTC
•	Target Device: Meta Quest 3
•	Action: Switch platform to Android
Step 2: Player Settings
•	Graphics API: Remove OpenGLES3; retain Vulkan
•	Package Name: com.DefaultCompany.Quest3MR
•	Minimum API Level: API Level 32
•	Scripting Backend: IL2CPP
•	Target Architecture: Check ARM64; uncheck ARMv7
Step 3: Meta OpenXR Unity Package
•	Add the package: "com.unity.xr.meta-openxr"
•	Restart Unity after installation
•	Automatically installs dependencies:
o	AR Foundation
o	OpenXR Plugin
o	XR Core Utilities
o	XR Legacy Input Helpers
o	XR Plugin Management
Step 4: Install XR Interaction Toolkit
•	Locate via Unity Registry
•	Install XR Interaction Toolkit
Step 5: Configure XR Plug-in Management
•	Platform: Android
o	Enable OpenXR
o	Enable Meta Quest Support feature group
•	OpenXR Subsettings
o	Under Enabled Interaction Profiles, enable Oculus Touch Controller Profile
o	Under Project Validation, address two key issues:
1.	AR Camera Manager Missing: Add AR Camera Manager component to Main Camera.
2.	Screen Space Ambient Occlusion (SSAO): Disable or remove this feature to optimize performance.
Step 6: Optimize URP and Quality Settings
•	Quality Settings:
o	Keep only the Balanced level; remove Performant and High Fidelity
o	Set VSync Count to Don't Sync
•	Graphics Settings:
o	Assign URP-Balanced as the default render pipeline
•	URP-Balanced Settings:
o	Disable Post-processing, HDR, Terrain Holes, and Additional Lights
o	Set shadow Max Distance to 2.5
o	Remove Global Volume from the Hierarchy
Step 7: Scene Setup
•	Delete the default Main Camera
•	Add: XR Origin (VR) → includes XR Interaction Manager
•	Set Tracking Origin Mode to Floor
•	Configure Main Camera:
o	Background Type: Solid Color
o	Background Color: RGBA(0, 0, 0, 0)
o	Add AR Camera Manager component
•	Add: AR Session to manage AR lifecycle
Step 8: Import Assets
•	Import zombie model from Unity Asset Store
•	Convert assets to URP using:
o	Window → Rendering → Render Pipeline Converter
•	Adjust zombie prefab:
o	Position Z: 1.5
o	Rotation Y: 180
•	Build and Run the project

1.2 Plane Detection
•	Import samples:
o	XR Interaction Toolkit → Samples → Import "Starter Assets" and "AR Starter Assets"
•	In Hierarchy:
o	Add AR Plane Manager to XR Origin (XR Rig)
o	Assign the AR Feathered Plane prefab to Plane Prefab
•	Build and run:
o	You will see detected planes (floor, ceiling, furniture)
o	Use controllers to place furniture
Input Settings for Controllers
•	Assign XRI LeftHand Controller and RightHand Controller to respective XR Controller components
•	In Input Action Manager, add XRI Default Input Actions
•	Disable XR Ray Interactor if using direct interaction

1.3 Debug Panel Design
To aid development and debugging in MR:
•	Add a debug UI panel in the scene:
o	Import a custom package or prefab
o	Adjust RectTransform: Y = 1.5, Z = 0.75 and not change others
•	Implement Plane Visualization:
o	Use ARPlaneMeshVisualizer, MeshRenderer, LineRenderer
o	LineRenderer emphasizes boundaries

1.4 Room Model Setup
•	Model the room using detected planes and spatial meshes
•	Define boundaries using line renderers and colliders
•	Establish normal for spatial alignment and object placement
•	Here, we use the prefab of ARPlaneColored.unitypackage from Ludic Worlds, which provides clearer and more apparent colors boundaries to help to set your room model

1.5 Interactable Object Setup via XR Direct Interactor
•	Configure the controller:
o	Remove XR Ray Interactor, Line Renderer, and Line Visual
o	Add XR Direct Interactor
•	Add a grabbable object:
o	In Hierarchy: Add Cube → Rename to "Grabbable Cube"
o	Add XR Grab Interactable component
o	Add Sphere Collider and check Is Trigger
•	Use the controller to pick and place objects in MR environment
•	Save prefab for reuse:
o	Drag Grabbable Cube into Assets → Prefabs

1.6 Final Build and Execution
•	Coordinate game logic:
o	Zombie AI behaviors
o	Player movement and input
o	Spatial interactions triggered by real-world positioning
•	Use Build and Run to deploy the game onto Meta Quest 3
