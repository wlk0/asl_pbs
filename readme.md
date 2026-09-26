A VASL extension for playing ASL PBS (Play Both Sides)
https://www.facebook.com/groups/358520268920548

### Version

Extension version: 1.00

ASL PBS rules reference: v32

### Credits

Author: Nicola Marangon

Base code derived from the SASL Activation Checking extension.

A big thank you to Andrea Fantozzi, author of the ASL PBS rules.

## Using the extension

The extension is loaded on top of a VASL game with an active ASL/VASL module, over the main map ("Main Map").

### Setup (required for the activation check to work)

Before playing, place one counter of each faction's nationality on the **PBS Sides** map (toolbar menu PBS → PBS Sides):

- Faction A: drop a counter on region `NatA1` and/or `NatA2`.
- Faction B: drop a counter on region `NatB1` and/or `NatB2`.

The nationality of the counters placed on these regions is what tells the extension which side is Faction A and which is Faction B. If this step is skipped, the automatic activation check will not be able to tell friend from foe and will not work correctly.

Optional, for night scenarios: place the `NVR` (Night Vision Range) counter on the **Scenario Aid Card** map. If it's not present there, the extension also looks for it on the main map.

### Automatic activation check

On every move (drag or keyboard) or rotation of a piece on the Main Map, the extension:
1. updates the nationalities of the two factions by reading the PBS Sides map;
2. updates the night status (NVR, illumination from Starshell/IR/Blaze);
3. computes the LOS from the moved pieces to the opposing faction's pieces;
4. applies the `*ACTIVATE? (R=n)*` label to enemy pieces that are within LOS (and within NVR range, if in effect), where `n` is the range.

### Windows, maps and counters provided by the extension

All accessible from the **PBS** toolbar menu:

- **PBS Sides**: where you place the faction-defining counters (see Setup above).
- **PBS Tracker Sheet**: scenario tracking counters — Victory Points (Axis/Allied), NVR, PF, TH, SAN (Axis/Allied), Battery A-D, No Quarter (Axis/Allied), Attacks.
- **PBS Aider**: quick combat-resolution aid counters — OFTC DRM, TH, TH DRM, MP (+10/+20/+30), Range Suppression/Interdiction, +1 next attack.
- **PBS Cloaking Display**: HIP tracking grid — Ambush/Surprise markers (A-J) and Surprise Control markers (K-T).
- **PBS Counters**: opens the "PBS" tab (under Other) in the VASL Counters palette, with all of the extension's markers available to drag onto the map — the Aider/Cloaking Display counters above, plus Motion Attempt, Next Action (Move/Pivot/VBM), Mines, Road Mines, Volume Firelane and the generic PBS Token.

### PBS Tables

A separate chart window ("PBS Tables" toolbar button) with reference tables: Generic, IFT First Fire, Ordnance First Fire, Hip & Concealment, Misc 1, Misc 2.

### Toolbar buttons (ASLPBSChecker)

- **PBS Reset**: removes all `*ACTIVATE?*` labels from the pieces.
- **PBS Disc.**: left click rolls 1d10 for Fire Discipline (IFT First Fire 2.1: modified result ≤3 = Interdiction, DRM -4 if the previous roll was already Interdiction); right click resets the indicator.
- **PBS Auto-Disc.**: when enabled, rolls Fire Discipline only if the move puts an enemy unit in LOS.
- **PBS Debug**: when enabled, prints diagnostic info to the chat (nationality, faction, NVR, illumination status) for every piece evaluated — useful during testing/development.

### Keyboard shortcuts (configurable)

- **Clear Flares** (default Ctrl+Alt+X): removes the `*ACTIVATE?*` labels and clears the stored "moving" pieces.
- **Check Activations** (default Ctrl+Alt+S): forces an activation check on the currently selected pieces.

### build the class
`javac --release 11 -d out -cp /home/nicola/fun-dev/vasl/target/classes:/home/nicola/fun-dev/vassal/vassal-app/target/classes src/ASLPBSChecker.java 
`

### build the class and deploy
`javac --release 11 -d /home/nicola/fun-dev/asl_pbs/out -cp /home/nicola/fun-dev/vasl/target/classes:/home/nicola/fun-dev/vassal/vassal-app/target/classes /home/nicola/fun-dev/asl_pbs/src/ASLPBSChecker.java && cd /home/nicola/fun-dev/asl_pbs/out && zip -u /home/nicola/Jottacloud/Vassal/vasl-6.7.2-beta4_ext/asl_pbs.vmdx VASL/build/module/ASLPBSChecker*.class`
