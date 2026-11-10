# Pavlov Shack | Custom Gun Development Guide

> Source: https://mod.io/g/pavlov/r/pavlov-shack-custom-gun-development-guide
> Author: jackpavlovmod2010 | Added: 2026-10-22 | Updated: 2026-10-22 | Views: 56 | Comments: 0 | Tags: none
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 0 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: Technical reference for creating custom weapons in the Pavlov Shack Mod Kit. Covers weapon Blueprints, gun states, generic flags, animation variables, charging handles, magazines and weapon mechanics, with examples from existing Pavlov guns.

---
Pavlov Shack – Gun Blueprint Technical Reference

**Last reserched in the**** | 22/10/2026**

### Generic Fields

-
`GenericScalar1/2` — Float

-
`bGenericFlag1/2/3` — Boolean

-
`GenericVector1/2` — Vector

-
Python: `generic_scalar1`, `generic_flag1`, etc.

-
Usage is **weapon-specific**, primarily animation-related.

### Verified Field Usage

|
Weapon |
Field |
Function |

|
M4 |
Scalar2 |
ReloadHandle X → Anim Select |

|
M4 |
Flag1 |
Handle grab / ungrab |

|
M4 |
Flag2 |
HasAttachment → Anim OR |

|
M4 |
Flag3 |
Name comparison → Float |

|
MG42 |
Scalar1 |
Dust-cover rotation / clamp |

|
MG42 |
Scalar2 |
`b_gun_belt` Y translation |

|
MG42 |
Flag1 |
BeltInPlace |

|
MG42 |
Flag2 |
Belt-grab blend |

|
MG42 |
Flag3 |
bHasMagazine |

|
PKM |
Scalar1 |
Dust-cover Roll |

|
PKM |
Scalar2 |
Belt animation |

|
PKM |
Flags1–3 |
Belt position / grab / magazine |

|
Revolver |
Flag1 |
Cylinder `bOpen` |

|
Revolver |
Flag2 |
Chamber/reset blend |

|
Shotgun |
Scalar1 |
UpdateChamber / pump calculations |

|
Shotgun |
Scalar2 |
Feeder-bone Alpha |

|
MP40 |
Scalar1 |
ReloadHandle X |

|
MP40 |
Flags1–2 |
Handle / action selectors |

|
Kar98 |
Flag1 |
Use / visibility animation |

|
M1A1 |
Flags/scalars |
Rocket / chamber state |

### Gun State Classes

|
State |
Example weapons |

|
`VRGunState` |
AK47, M4, M9, MP40, MP5, MG42, PKM, M1 Garand, M1A1 |

|
`RifleGunState` |
Kar98 |

|
`RevolverGunState` |
Revolver |

|
`PumpActionGunState` |
Shotgun |

### Implementation Notes

-
Trace `Event → Field Write → AnimBP Reader → Bone/Blend`.

-
Preserve original field assignments and reset events.

-
Check timelines, clamps, selectors and bone transforms.

-
Generic fields have **no universal meaning** across weapons.

-
Replication/authority behaviour is not confirmed.

-
Use custom named variables unless native/inherited logic requires generic fields.

-
Reference documents contain exact defaults, graph connections and node-pin values.
