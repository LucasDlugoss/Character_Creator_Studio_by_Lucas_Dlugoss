# Character Creator Studio by Lucas Dlugoss

Turn a text prompt or reference images into a textured 3D asset, with optional automatic rigging and an editable Blender file.

Lucas Character Studio is a free local app built on ComfyUI by Lucas Dlugoss. Its guided interface takes you through reference creation, view approval, 3D generation, PBR painting, and optional UniRig rigging. You can open the ComfyUI node editor whenever you need it.

Generation runs on your own hardware once the required models and dependencies are installed. Initial setup and model downloads require an internet connection.

☕ Support development on Ko-fi
Features
- Text or image input: describe your asset or upload at least one reference view.
- Three generated views: front, left, and back, with approval before 3D generation.
- Additional uploaded views: front, left, back, right, top, and bottom. Top and bottom are used for PBR painting.
- Anatomy presets: guide the reference pose for different body plans, including non-humanoid characters.
- PBR textures: Base Color, Metallic, and Roughness, exported with the model.
- Optional UniRig: predict a skeleton and skin weights for further editing in Blender.
- Editable Blender output: packed textures and connected shader nodes, with or without a rig.
- Performance controls: Automatic, Speed, Quality, and Manual profiles.
- Guided interface: progress feedback, tips, reference review, and access to the node editor.
- Eight interface languages: English, Brazilian Portuguese, Spanish, French, German, Italian, Simplified Chinese, and Japanese.
Requirements
Component	Requirement
Operating system	Windows x64
Host application	An existing ComfyUI Desktop installation
GPU	NVIDIA GPU with CUDA support
Automatic profile memory threshold	Approximately 16 GB VRAM and 32 GB system RAM
Blender	Version 4.2 or later for .blend export and rig finalization
Storage and internet	Space for model weights, dependencies, and outputs; internet access for downloads
Native PBR build tools	Visual Studio C++ Build Tools and a compatible CUDA Toolkit may be required


These memory thresholds are profile eligibility checks, not guaranteed minimum requirements for every generation. Actual usage depends on models, resolution, available memory, and rig settings. Manual mode does not guarantee that smaller GPUs will work.
Installation
1. Close ComfyUI.
2. Download the app package and extract the entire ZIP into a folder. If using the repository source, keep its directory structure intact.
3. Run INSTALL.cmd. Keep the window open until setup finishes.
4. Open ComfyUI, refresh the interface with Ctrl+F5, and import Qwen_Character_Approval_3Views_Offline.json into a new tab.
The installer uses your existing ComfyUI Desktop installation on Windows. It prepares Git, Blender, and the UniRig environment when needed. Downloads require internet access and free disk space. The Qwen/Hunyuan generation models and their nodes must be available. PBR painting requires its native extensions; compiling them may require Visual Studio C++ Build Tools and the CUDA Toolkit. Installation errors are recorded in lucas_install_logs. Do not enable rigging until its installation is complete.
Using the app
Choose your interface language, then enter a description and select an anatomy preset, or upload reference images. Image generation produces front, left, and back views. Upload mode accepts additional references; top and bottom views are used for painting. Approve the views, choose a performance profile, and run generation. UniRig is optional.

Automatic and Quality adjust parameters according to detected memory. Check the effective settings shown in the interface. Manual uses the performance node's manual_* parameters. No profile guarantees compatibility with every GPU.

Click Open editor to see the ComfyUI nodes and load another workflow. Save any changes to your current workflow first.
Blender files and materials
After generation finishes, use the editable Blender file download button. The .blend includes packed images and a material connected to the Principled BSDF:
- Base Color: an sRGB image connected to Base Color.
- Metallic: a Non-Color image connected to Metallic.
- Roughness: a Non-Color image connected to Roughness.
- If only the combined map is available, its green channel provides Roughness and its blue channel provides Metallic.
The individual maps and the combined map represent the same data; they are not added together. The current painting pipeline does not generate normal, displacement, or ambient occlusion maps. The material does not invent this information. The mesh retains its original UVs and uses an Alpha value of 1.

The GLB includes PBR materials and can be imported through File > Import > glTF 2.0. To inspect the explicit shader node connections, open the .blend and select the object in the Shading workspace. Use Material Preview or Rendered shading.

The .blend is created with or without a rig and requires Blender 4.2 or later. When rigging is enabled, it also includes the skeleton and skin weights. Check deformations before animating. Blender export failures preserve the original GLB and create a .log file alongside it.

Files are saved in ComfyUI's output directory, normally under Lucas_Character/3D. Outputs include a GLB, PNG maps, reports, and a .blend. The .blend contains its images and can be moved on its own.
Resuming stages
- Lucas_Retomar_PBR.json: repaints from a saved checkpoint without rebuilding the geometry.
- Lucas_Retomar_Rig.json: accepts the relative path of a GLB inside the output directory. UniRig adds a rig; None prepares a .blend without a rig.
Older GLBs without associated PNG files retain their embedded materials. Keep each model's PNG files alongside its GLB to reconstruct the explicit material connections. Do not rename only part of the file set.
Getting better results
- Use references of the same subject with matching proportions, pose, and scale.
- Keep the entire subject visible against a simple background, with space around limbs and extremities.
- Choose an anatomy preset that matches the subject. Avoid humanoid pose instructions for animals.
- Review every reference before generating the mesh. Conflicting views can produce incorrect geometry and texture seams.
- Check the effective texture settings when selecting a performance profile. Quality settings remain constrained by available memory.
- Inspect skin weights and test joint movement in Blender before animation.
Limitations
Generated geometry, textures, and rigs may require manual cleanup. Automatic rigging does not guarantee correct joints or deformation for every anatomy, and does not provide a complete animator control rig with IK or facial controls. The app does not guarantee animation-ready retopology or game-ready assets.

Material connections do not increase texture resolution or repair artifacts already present in the mesh or images. This package does not generate normal, displacement, or ambient occlusion maps.
Troubleshooting
- Missing nodes or models: check the ComfyUI startup log and confirm that the required Qwen/Hunyuan nodes and model files are installed.
- PBR installation failure: keep the full log from lucas_install_logs and resolve the reported native extension or build-tool error before painting.
- Rig setup incomplete: leave rigging disabled until UniRig and Blender setup succeeds.
- Interface not updated: restart ComfyUI and refresh with Ctrl+F5.
- Blender export failure: inspect the .log beside the original GLB. The original GLB is preserved.
When reporting a problem, include your GPU and VRAM, system RAM, ComfyUI version, selected performance profile, the failed stage, and the full relevant error log. Remove private paths or information before posting publicly.
Support development
Enjoyed bringing your idea to life? If this app helped you, you can buy me a coffee and help me keep building free AI tools. Your support means a lot!

☕ Buy Lucas a coffee on Ko-fi

Contributions are completely optional and do not unlock or restrict any app features or downloads.
Licenses and credits
Qwen, Hunyuan3D, UniRig, ComfyUI, and Blender retain their own licenses. See THIRD_PARTY_NOTICES.txt and the licenses of the installed components. Model weights and binaries are downloaded from their distributors and are not included in this package.

Free access to this app does not replace or override the licenses of its dependencies or model weights. Review their terms before commercial use or redistribution.
