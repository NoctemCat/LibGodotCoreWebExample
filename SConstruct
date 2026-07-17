#!/usr/bin/env python
import os
import sys

from methods import print_error


editor_shared_libgodot_name = "libgodot.linuxbsd.editor.x86_64.llvm"


localEnv = Environment(tools=["default"], PLATFORM="")

customs = ["custom.py"]
customs = [os.path.abspath(path) for path in customs]

opts = Variables(customs, ARGUMENTS)
opts.Update(localEnv)

Help(opts.GenerateHelpText(localEnv))

env = localEnv.Clone()

if not (os.path.isdir("godot-cpp") and os.listdir("godot-cpp")):
    print_error("""godot-cpp is not available within this folder, as Git submodules haven't been initialized.
Run the following command to download godot-cpp:

    git submodule update --init --recursive""")
    sys.exit(1)

env = SConscript("godot-cpp/SConstruct", {"env": env, "customs": customs})


env.Append(LIBPATH=["godot/bin"])
env.Append(LIBS=[editor_shared_libgodot_name])

env.Append(CPPPATH=["src/"])
sources = Glob("src/*.cpp")

program = env.Program(f"bin/{env["platform"]}/libgodot_editor", source=sources)

libgodot = env.Install("bin/", [program, f"godot/bin/{editor_shared_libgodot_name}{env.subst('$SHLIBSUFFIX')}"])

Default(program, libgodot)
