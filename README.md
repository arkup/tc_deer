# tc_deer - **T**ri**C**ore <b>De</b>compil<b>er</b> plugin for IDA pro

**Description**
_______________________________

A TriCore (ASM → C decompiler) plugin for IDA pro, currently in beta. Results vary: some samples decompile well, others may fail.

The release zip contains an engine .dll and a Python presenter script. The presenter formats JSON from the engine, since the code wasn't originally an IDA plugin, I hacked in a Qt TextEdit tab with coloring.

The engine source is messy and not released, it needs significant cleanup and refactoring.

Windows build only, compiled for **IDA Pro 9.2**.

Bugs or suggestions? Please open a GitHub issue.

_______________________________
**1.0 Install - Copy the configuration file**
_______________________________

Copy `tc_deer_plugin_conf.ini` to your Hex-Rays\IDA plugins user directory:

`%APPDATA%\Hex-Rays\IDA Pro\plugins`

Example path: `C:\Users\[YOUR_USERNAME]\AppData\Roaming\Hex-Rays\IDA Pro\plugins`

_________________
**1.1 Update the configuration file paths to the decompiler engine .dll**
_________________

Open `tc_deer_plugin_conf.ini` and adjust the paths under [Settings] to point to engine dlls.

Example:
```
[Settings]

WRAP_DASM_PATH      = c:/ida_plugins/tc_deer/wrap_disasm.dll
CAPSTONE_PATH       = c:/ida_plugins/tc_deer/capstone.dll
TRI_DECOMPILER_PATH = c:/ida_plugins/tc_deer/tri_dec_eng.dll
ENABLE_LINKS        = true
```
_________________
**1.2 Copy the interface script to IDA plugins folder**
_________________

Copy the presenter `tc_deer_presenter.py` script into the IDA 9.2 plugins folder.

Example: `C:\Program Files\IDAPro92\plugins\tc_deer_presenter.py`

_______________________________
**2. Usage**
_______________________________

Launch IDA and open a Tricore binary file.
Navigate to a function, then press **Ctrl+Shift+B** (or Edit->Plugins->Tricore plugin) to decompile the currently disassembled function.

Double click to highlight variables.
Press `Tab` to switch to the matching assembly line in the disassembly view.

_______________________________
**Limits:**
_______________________________

- not all TriCore instructions are supported
- `switch()` statements aren't supported, as they require a preprocessing step to extract the jump table before decompilation
- floating point instructions are not supported
- handling of qword operations needs improvement
- ...
- and many bugs that either did not appear in my test cases or had to be postponed due to time constraints

_______________________________
**Credits:**
_______________________________

- This project uses the [Capstone disassembly framework](http://www.capstone-engine.org/)
