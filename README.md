# LibGodot Core Web Export Example

This example only supports web export templates, but it should be possible to build web editor, there is just no code for it.
Brings web LibGodot on par with currently implemented platforms.

## How to build

Steps:
- Update git submodules
```
git submodule update --init
```
- Build shared LibGodot editor. Pick the platform you develop on https://docs.godotengine.org/en/stable/engine_details/development/compiling/index.html and install requirements
```
cd godot
scons target=editor library_type=shared_library
cd ..
```
- Change `editor_shared_libgodot_name` in root `SConstruct` to the name of the resulted shared library without shared library suffix
- Build editor in root
```
scons target=editor
```
- Launch `bin/libgodot_editor` and open the `project` folder, try to launch the project in editor, it should work
- Install Emscripten https://emscripten.org/docs/getting_started/downloads.html#installation-instructions-using-the-emsdk-recommended , this example used version 5.0.6
- Build shared web export templates, the same as https://docs.godotengine.org/en/stable/engine_details/development/compiling/compiling_for_web.html , but with `library_type=shared_library`
```
cd godot
scons platform=web target=template_debug library_type=shared_library
scons platform=web target=template_release library_type=shared_library
cd ..
```
- Build web export templates in root
```
scons platform=web target=template_debug
scons platform=web target=template_release
```
- Export web platform in editor, the relative path for custom templates should work now