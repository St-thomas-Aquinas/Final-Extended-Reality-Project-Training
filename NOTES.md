MUT TECH COMMUNITY TRAINING FOR EXTENDED REALITY

#
1️⃣ Creating a Skybox
1.1 Create a Skybox Material
1.	In the Project window
2.	Right-click → Create → Material
3.	Name it Skybox_MyWorld
________________________________________
1.2 Change the Material Shader to Skybox
1.	Select the material
2.	In the Inspector, set:
o	Shader → Skybox → 6 Sided
Alternatives:
•	Skybox → Cubemap
•	Skybox → Procedural
________________________________________
1.3 Add Skybox Textures
For a 6-Sided Skybox, assign textures to:
•	Front
•	Back
•	Left
•	Right
•	Up
•	Down
👉 Use seamless sky images (clouds, space, sunset, etc.)
________________________________________
1.4 Apply the Skybox to the Scene
1.	Go to Window → Rendering → Lighting
2.	Under Environment
3.	Drag your Skybox material into Skybox Material
✅ The skybox appears instantly in Scene and Game view.
________________________________________
2️⃣ Creating a Planet
2.1 Create a Sphere
1.	Hierarchy → Right-click → 3D Object → Sphere
2.	Position it in your scene
________________________________________
2.2 Import Your Image
1.	Drag your image into the Project window
2.	Select the image and set in Inspector:
o	Texture Type: Default
o	Wrap Mode: Repeat
o	Filter Mode: Bilinear or Trilinear
3.	Click Apply
________________________________________
2.3 Create a Material
1.	Right-click → Create → Material
2.	Name it (e.g. Earth_Material)
3.	Set Shader:
o	Standard (Built-in)
o	or URP/Lit (URP projects)
________________________________________
2.4 Apply the Image to the Material
1.	Drag the image into Base Map / Albedo
2.	Drag the material onto the Sphere
✅ The image wraps correctly around the planet.
________________________________________
3️⃣ Planet Orbit, Self-Rotation & Scene Change
Step 1: Scene Setup
1.	Create an empty GameObject → name it Sun
2.	Create a Sphere → name it Planet
3.	Attach the script below to Planet
4.	Assign:
o	Center Object: Sun
o	Scene To Load: target scene name (must be in Build Settings)
________________________________________
Step 2: C# Script — PlanetOrbit.cs
using UnityEngine;
using UnityEngine.SceneManagement;

public class PlanetOrbit : MonoBehaviour
{
    [Header("Orbit Settings")]
    public Transform centerObject;
    public float orbitSpeed = 20f;

    [Header("Self Rotation Settings")]
    public float rotationSpeed = 50f;

    [Header("Scene Settings")]
    public string sceneToLoad;

    void Update()
    {
        // Orbit around the sun
        if (centerObject != null)
        {
            transform.RotateAround(
                centerObject.position,
                Vector3.up,
                orbitSpeed * Time.deltaTime
            );
        }

        // Rotate on its own axis
        transform.Rotate(Vector3.up, rotationSpeed * Time.deltaTime);
    }

    void OnMouseDown()
    {
        if (!string.IsNullOrEmpty(sceneToLoad))
        {
            SceneManager.LoadScene(sceneToLoad);
        }
    }
}
________________________________________
Step 3: Enable Scene Loading
1.	File → Build Settings
2.	Click Add Open Scenes
3.	Ensure the target scene is listed
________________________________________
Step 4: If Clicking Doesn’t Work
Check that:
•	The planet has a Collider (Sphere Collider)
•	The Camera is not blocking raycasts
•	No UI elements are covering the planet
________________________________________
4️⃣ Creating a Mars-Like Terrain 🟥
4.1 Create Terrain
1.	Hierarchy → Right-click → 3D Object → Terrain
2.	Select the Terrain object
________________________________________
4.2 Shape the Terrain (Mars Style)
In Inspector → Terrain Tools:
•	Raise / Lower Terrain
o	Brush Size: 30–60
o	Opacity: 0.2–0.4
o	Create hills and craters
•	Smooth Height
o	Light smoothing (Mars is rugged but soft)
•	Noise Tool
o	Low-frequency noise
o	Creates rocky, uneven ground
🧠 Tip: Avoid sharp mountains — Mars terrain is eroded and dusty.
________________________________________
4.3 Apply Mars Ground Textures
Import Textures
Recommended textures:
•	Red sand
•	Rocky dirt
•	Dark basalt
Create Terrain Layers
1.	Terrain Inspector → Paint Texture
2.	Edit Terrain Layers → Create Layer
3.	Assign Mars texture
4.	Adjust:
o	Tile Size: 10–30
o	Tile Offset: slight variation
🎨 Blend 2–3 textures for realism.
________________________________________
4.4 Lighting for Mars
•	Directional Light
o	Color: soft orange / warm red
o	Intensity: 1 – 1.3
•	Disable strong blue lighting
________________________________________
5️⃣ Procedural Mars Skybox 🌌
5.1 Create Skybox Material
1.	Right-click → Create → Material
2.	Name it Mars_Skybox
3.	Shader → Skybox → Procedural


________________________________________
5.2 Mars Skybox Settings
Setting	Value
Sun Size	0.02
Sun Size Convergence	5
Atmosphere Thickness	0.3 – 0.5
Sky Tint	Reddish-brown
Ground Color	Dark red / brown
Exposure	1.1 – 1.4
☁️ Mars has a thin atmosphere, so keep it dim and dusty.
________________________________________
5.3 Apply the Skybox
1.	Window → Rendering → Lighting
2.	Drag Mars_Skybox into Skybox Material
3.	Click Generate Lighting
________________________________________
6️⃣ Mars Fog & Atmosphere (Very Important)
1.	Window → Rendering → Lighting
2.	Enable Fog
3.	Settings:
o	Color: light orange / dusty red
o	Mode: Exponential
o	Density: 0.01 – 0.03
🌫 Creates realistic Martian dust haze.

