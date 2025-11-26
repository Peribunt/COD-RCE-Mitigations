# MW2 2009 Known RCE Mitigations

These are all the documented RCE mitigations for MW3 2011. This repository only includes mitigations for RCE exploits that are currently active on the game.
An executable that makes all patches for these exploits accessible is included.

## UI_ReplaceDirective
`UI_ReplaceDirective` gets used for various purposes within a multitude of COD games. In this case it can be exploited to cause a stack buffer overflow. This can be achieved through server commands and other HUD related things that can be sent from the host to clients.

![UI_ReplaceDirective](https://github.com/Peribunt/COD-RCE-Mitigations/blob/main/iw4mp/Resource/UI_ReplaceDirectiveVuln.png)

### How to fix

Fixing this can easily be done by hooking or patching `UI_ReplaceDirective` to perform a boundary check on the source string.
If it contains `[{` and at any point the length of the string following those characters exceeds 256, it should exit prematurely.

![UI_ReplaceDirective](https://github.com/Peribunt/COD-RCE-Mitigations/blob/main/iw4mp/Resource/UI_ReplaceDirectiveProt.png)
