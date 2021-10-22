# NCams/AAH OpenSim upper limb musculoskeletal model

AAH is a musculoskeletal model of human upper limb (shoulder, arm and hand) for inverse kinematics. It is based on the [ULB project](https://simtk.org/projects/ulb_project), has 32 body segments (plus 3 phantom and 22 muscle-supporting), 29 moving DOFs and 10 fixed (weld) joints. We aim to maintain a model that could be easily used by any researcher in need of calculation of upper limb inverse kinematics or muscle lengths.

The model is an out-of-box solution for calculation of inverse kinematics and does not include dynamic properties (e.g. inertia or mass). In the current form it is not suited for dynamic simulations in OpenSim. The muscle paths were also unchanged and contain [inconsistencies](https://www.biorxiv.org/content/10.1101/2020.05.29.124644), however it is the best available model of the hand musculature to our knowledge (for purely arm model see [MoBL-ARMS](https://simtk.org/projects/upexdyn)) . An example of the model's use can be found in the [NCams](https://github.com/CMGreenspon/NCams) project. 

We welcome any contributions or suggestions. This model can be found on [GitHub](), [OpenSim]() and (in part) in [NCams]() repository. 

## Plans for the future

As most researchers, we develop models when we need them. If you feel like developing a model for your own experiments, consider publishing these changes and the new, improved model here.

* Improve description of proximal movement and musculature by including [MOBL](https://simtk.org/projects/upexdyn).
* Improve wrist, thumb and index finger by including [Wrist Model](https://simtk.org/projects/wrist-model).
* Add movement of 4th and 5th carpometacarpal rays.

## List of changes

1. Update to OpenSim 4.3.
2. Split model into unimanual. The lower body as well as contralateral limb were removed. Left and right models are equivalent.
3. Renaming of the objects. To simplify and improve the joint and body naming distal to the shoulder, we adopted the following schema after [Sobinov et al., 2020](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1008350) and [Boots et al., 2020](https://www.biorxiv.org/content/10.1101/2020.05.29.124644). A full list of body, joint and DOF names can be found in the .csv files.

    1. Limb [_bodies_](AAH%20Model/bodies.csv) are named `<LIMB><DIST><BONE_LITERA><DIGIT_NUMBER>`, where:

        * `LIMB` corresponds to the limb where the body is located, i.e. ‘RA’ stands for ‘right arm’ (CSV files omit the R/L letters), 
        * `DIST` - approximate number of segments separating this segment from the torso in the kinematic chain (humerus - 1, forearm - 2, wrist - 3, metacarpal - 4, etc.), 
        * `BONE_LITERA` - a single letter based on the anatomical name of the bone, 
        * `DIGIT_NUMBER` - 1 thumb; 2 index; 3 middle; 4 ring; and, 5 pinky. Phalanxes are marked as P: proximal, M: middle, D: distal. 
    A few examples: RA1H - right arm humerus, LA3L - left arm lunate carpal bone, RA4M1 - first (thumb) metacarpal of the right hand, RA7d5 - distal pinky phalanx.
    2. [_Joints_](AAH%20Model/joints.csv) are named based on the bodies they connect: `<PARENT BODY>_<CHILD_BODY>`, e.g., RA3T_RA4M1 - carpometacarpal joint of the right thumb, LA4M4_LA4P4 - metacarpophalangeal joint of the left hand. Weld (fixed) joints additionally get a `_W` postfix.
    3. [_DOFs_](AAH%20Model/dofs.csv) are named based on the anatomical name of the joint and the direction of movement: `<LIMB>_<JOINT>_<MIN>_<MAX>`, where:

        * `JOINT` is the anatomical name of the joint containing this DOF, e.g., ‘wr’ is ‘wrist’. Digit joints have their identifying number: 1 thumb; 2 index; 3 middle; 4 ring; and, 5 pinky. 
        * The last two suffixes MIN and MAX indicate the anatomical direction of axis, e.g., ‘ra_wr_s_p’ indicates the range of the wrist pronation-supination DOF (negative values for the supinated postures and positive - for the pronated posture). 
        * Dependant coordinates are marked with `_d`.
4. Additional hand DOFs.
    1. `cmc1_opp` - opposition (rotation) around thumb carpometacarpal joint.
    2. Digits 3-5 metacarpophalangeal flexion-extension and abduction-adduction. Middle finger abduction-adduction was named radioulnar deviation to avoid confusion. Were modelled after index finger joints
    3. Digits 3-5 proximal and distal interphalangeal joints' flexion and extension. Were modelled after index finger joints.
5. Changes to ranges of motion.
    1. `ip1_e_f` - from \[-75° 25°\] to \[-75° 75°\].
    2. `mcp2_ad_ab` - from \[-15° 15°\] to \[-15° 30°\].
    3. `dip2_e_f` - from \[0° 90°\] to \[-30° 90°\].

## List of included models

* [RightArmAndHand](AAH%20Model/RightArmAndHand.osim) - model of the right arm and hand.
* [LeftArmAndHand](AAH%20Model/LeftArmAndHand.osim) - model of the left arm and hand.

## Contributors

- [**Anton Sobinov**](https://github.com/nishbo)
- [**James Goodman**]()
- [**Russell Hardesty**]()
