# MW3 2011 Known Active RCE Mitigations
These are all the documented RCE mitigations for MW3 2011. This repository only includes mitigations for RCE exploits that are currently active on the game.
An executable that makes all patches for these exploits accessible is included.

## MemberJoin
The MemberJoin RCE makes used of a vulnerable `MSG_ReadData` call on a stack allocated buffer in the function `PartyAtomicHost_HandleMemberJoin`. Sending a crafted `memberJoin` packet can very easily permit arbitrary code execution.

![MemberJoin Vulnerability](https://github.com/Peribunt/COD-RCE-Mitigations/blob/main/iw5mp/Resource/MemberJoinVuln.png)

### How to fix
Fixing this is quite simple, simply hook a point where the length of the vulnerable `MSG_ReadData` is accessible, and perform a boundary check.
In this example I am hooking MSG_ReadData itself and checking if the return address matches up with the return address within `PartyAtomicHost_HandleMemberJoin`

![MemberJoin Fix](https://github.com/Peribunt/COD-RCE-Mitigations/blob/main/iw5mp/Resource/MemberJoinProt.png)
