Building For Windows
====================

.. warning:: This page assumes you have basic understanding of
    C++ and `CMake <https://cmake.org/>`_




Getting The Source
------------------

To get Sowa Engine source code, you can download source
code on `GitHub <https://github.com/sowaengine/sowa>`_ 
or clone it via `git <https://git-scm.com/>`_ version
control system

To clone it, if you are using git CLI, enter the following command in
terminal

.. code-block:: bash

    git clone https://github.com/sowaengine/sowa.git --recurse-submodules

.. attention:: -\-recurse-submodules is important because the engine
    uses submodules. If you forgot to add that parameter, you can run
    the following command after cloning

.. code-block:: bash
    
    git submodule update --init --recursive --remote

Generating Resources
^^^^^^^^^^^^^^^^^^^^

Built-in resources in Sowa Engine are generated using `nmres <https://github.com/Lexographics/nmResource>`_ tool
You can install latest version of it `here <https://github.com/Lexographics/nmResource/releases/>`_

After downloading nmres, run the following command in engine root directory

.. code-block:: bash
    
    /path/to/nmres.exe --recursive --cwd Sowa --namespace Sowa::Res \
        --suffix .res.hpp --rules res_rules.txt

this will generate necessary resources in project

|

Building The Engine
-------------------

Requirements
^^^^^^^^^^^^

* `MinGW-w64 <https://www.mingw-w64.org/>`_ or `clang <https://clang.llvm.org/>`_
* `CMake <https://cmake.org/>`_


Setting Up CMake
^^^^^^^^^^^^^^^^

Sowa Engine uses CMake for generating project files. You can generate
a MinGW project using the following command:

.. code-block:: bash

    cmake -S . -B build/ -G "MinGW Makefiles"



:guilabel:`-S`
    Source directory will be passed to this parameter.

:guilabel:`-B`
    Build directory will be passed to this parameter.

:guilabel:`-G`
    | Build system to generate project files.
    | ``"MinGW Makefiles"`` is preferred
    | You can see `possible generator options here <https://cmake.org/cmake/help/latest/manual/cmake-generators.7.html>`_

:guilabel:`[-D ...]`
    Used to pass options or parameter to cmake project.
    Here is some useful options

    | -DEditor -> On or Off (Default: On)
    | -DCMAKE_BUILD_TYPE -> Release or Debug (Default: Debug)

.. attention:: Editor option is On by default. Setting it to Off will
    generate export templates. (non-editor builds that will be used for
    exported projects)

Compiling Generated Project
^^^^^^^^^^^^^^^^^^^^^^^^^^^

After generating project via cmake, you can execute following command
to start compiling the engine

.. code-block:: bash

    cmake --build build/

To run multiple instances, you can execute the following command with
'n' being count of instances to run

.. code-block:: bash

    cmake --build build/ --parallel n


Installing The Engine
^^^^^^^^^^^^^^^^^^^^^

After compilation, build folder can look unorganized. To start
using the engine, you can copy executable ``sowa.editor.exe``, 
all content in ``ProjectManager/`` to a folder, and ``Editor/`` content in
``ProjectManager/`` folder

Directory structure should look like this:

| Sowa
| ├─Editor/
| │ ├─sowa.editor.lua
| │ └─sowa.editor.exe
| ├─sowa.engine.exe
| ├─project.ease (ProjectManager)
| └─project-manager-files
