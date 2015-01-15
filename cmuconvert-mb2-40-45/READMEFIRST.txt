        READMEFIRST v1.1, last update June 26, 2010 by B. Hahne

This READMEFIRST file accompanies the second (2010)
Motionbuilder-friendly BVH conversion release of the Carnegie-Mellon
University (CMU) Graphics Lab Motion Capture Database.  See "Where to
find stuff" at the bottom of this file for where to get the BVH
conversion and/or the original CMU dataset.

I released the original Motionbuilder-friendly BVH conversion in 2008.
This 2010 release is very similar, but has a few minor adjustments to some
of the joint rotations of the frame-one T pose which are intended to
make retargeting look slightly better in most cases.  This 2010
release doesn't touch any of the other frames and doesn't change the
Motionbuilder-friendly joint naming convention of the 2008 release.
In general, you'll probably want to use this 2010 release.

The original CMU motion capture database isn't in BVH format - it's
in ASF/AMC format.  This BVH conversion release was created by Bruce
Hahne, a hobbyist animator, in the interest of making the data more
available and easily usable by other animators.  I presently (2010)
maintain the web site www.cgspeed.com, where this BVH conversion
release is available within the motion capture section.

The emphasis on this release is to produce BVH files that can rapidly
be used in MotionBuilder for motion retargetting.  The files are not
particularly Poser-friendly or DazStudio-friendly, due to
incorrect assumptions that those programs have to make about the
underlying joint rotation setup.  A conversion for use with Daz
characters is in its early stages as of June 2010.



ADVANTAGES OF THIS RELEASE OVER THE ORIGINAL CMU DATA:
- This release has the motions in BVH format.

- T-poses: Every BVH file has a T-pose added as its new first frame.
  The T-poses face the positive Z axis and are therefore MotionBuilder
  compatible.

- Joint renaming: As many joints as possible have been renamed to be
  compatible with MotionBuilder's joint naming conventions.  This renaming
  makes it much easier (faster) to use the BVH files in MotionBuilder.

- Index files: The release includes consolidated indexes that list
  the motion filenames and their descriptions.  Both spreadsheet and 
  word processor friendly index files are available.

- MotionBuilder-friendly: the joint renaming and the addition of the
  T-pose make it possible to use these motions for animation
  retargetting within MotionBuilder in seconds rather than minutes.


COMPARISON OF THE 2008 AND 2010 MOTIONBUILDER-FRIENDLY RELEASES:

The original CMU BVH files don't provide T poses, which means it's
impossible to determine or recover the exact physical rotation of the
human actor's joints when the motions were recorded.  The situation is
made worse by the fact that the data is recorded using many different
subjects, and was presumably captured over multiple days or weeks with
different people operating and calibrating the motion capture
equipment.  The best that we can do is make a guess at a T pose, using
joint rotations that visually look like a T pose, but then adjusting
empirically so that we end up with retargeted animation that avoids
some of the most glaring flaws, such as elbows intersecting hips and
feet intersecting each other.  This 2010 release modifies the original
T pose slightly, based on my experiments with retargeting the CMU BVH
data onto one of the Daz characters.

For both the 2008 and 2010 Motionbuilder-friendly releases, the T pose
that I've added is in frame 0.  All other frames are from the original
CMU capture sessions.

- The 2008 release set the Z rotations of the upper arm joints
  ("RightArm" and "LeftArm" in MotionBuilder's naming convention) to 5
  degrees and -5 degrees respectively, to reduce problems with
  retargeted animation bending the arms down too much.  In the 2010
  release, I've changed these values to 8 and -8 degrees, which
  increases the level of compensation slightly.

- The 2008 release set the Z rotations of the upper leg joints
  ("RightUpLeg" and "LeftUpLeg" in Motionbuilder's naming convention)
  to 17 and -17 degrees respectively, to reduce problems with
  retargeted animation bending the legs in towards each other too
  much.  In the 2010 release, I've changed these values to 21 and -21
  degrees, which increases the compensation slightly.

- The 2008 release set all neck and head joint rotations to zero,
  which looks good visually within Motionbuilder but typically results
  in characters who have their neck bent far forward when you
  retarget.  The 2010 release uses non-zero X rotations on the neck
  and head joints, in an effort to provide a T-pose for the head which
  is probably closer to what the joint readings would have been when
  the original motion capture actors looked straight ahead.  The
  values in the 2010 release, for the Motionbuilder joints, are:
  	 Neck:  X rotation = -16 degrees
	 Neck1: X rotation = 21 degrees
	 Head:  X rotation = 11 degrees
  The net result of this compensation is to rotate the head up by
  about 15 degrees in retargeted animation, compared to use of the
  2008 BVH release.  However, for some of the BVH files you might find
  that you need to tilt the head up even more than this.


CONVERSION PROCESS:

- I started with the full set of AMC and ASF files, available from CMU
  as a single .zip file
- I ran the AMC/ASF files through amc2bvh in batch mode to produce BVH files.
- I analyzed several of the BVH files in MotionBuilder to determine how
  to set joint angles to set a T-pose.
- I then ran the BVH files through a Python script that I wrote to do
  joint naming conversion and T-pose generation.  This script is unreleased.
- With the exception of the new frame 1 (the T-pose), there are no
  modifications to the motion data itself.  If the original CMU data
  is noisy, the conversion will be noisy.  If the original CMU data
  has the actor's head moving at an impossible angle, the conversion
  will do the same.


CONVERSION NOTES:

Shoulders: The CMU dataset's skeleton is somewhat annoying around the
shoulders because it doesn't use a clavicle joint, only a shoulder
joint.  Also, the rotation points of the CMU skeleton shoulders are
significantly wider than the hips.  The result was that when I did
some retargetting tests in MotionBuilder, I often found that the
geometry of the target character's arms would punch through the hips.
To somewhat mitigate this problem, I set the T-pose of this converted
CMU dataset such that the arms angle slightly downwards, at 5 degrees
down from the horizontal.  This adjustment helps to reduce the "arms
through the hips" problem.


Fingers:  CMU's main page says this about the dataset:

  The "finger" and "thumb" joints are added to the skeleton for editing
  convenience - we do not actually capture these joints' motions and any
  such data should be ignored.

Therefore in the BVH joint naming conversion, I've maintained the
mapping "lfingers" to "LFingers" and "lthumb" to "LThumb", since these
are names that MotionBuilder's character joint naming convention does
NOT recognize.  We don't want MotionBuilder to try to use these joints,
since they have no data on them.


Playback speed: The CMU dataset was sampled at 120fps, however this
information apparently isn't saved in the CMU-distributed AMC/ASF
files, and the freeware utility amc2bvh simply assumes a default value
of 30fps (Frame Time = .033333) when it writes out BVH files.  This
BVH conversion release fixes the problem by rewriting Frame Time to
.0083333 in each BVH file, which equates to 120fps.


INDEX/INFORMATION FILES: 

Each .zip file in this BVH conversion release should include a copy of
this READMEFIRST.txt file, plus four variations of the same motion
index information:
- cmu-mocap-index-spreadsheet.ods: Open Document / OpenOffice
  spreadsheet format
- cmu-mocap-index-spreadsheet.xls: Microsoft Excel format
- cmu-mocap-index-txt.txt: A simple text file with the index
  information and no commentary.
- cmu-mocap-index-text.rtf: Rich Text Format index information with
  some commentary.


USAGE RIGHTS:

CMU places no restrictions on the use of the original dataset, and I
(Bruce) place no additional restrictions on the use of this particular
BVH conversion.

Here's the relevant paragraph from mocap.cs.cmu.edu:

  Use this data!  This data is free for use in research and commercial
  projects worldwide.  If you publish results obtained using this data,
  we would appreciate it if you would send the citation to your
  published paper to jkh+mocap@cs.cmu.edu, and also would add this text
  to your acknowledgments section: "The data used in this project was
  obtained from mocap.cs.cmu.edu.  The database was created with funding
  from NSF EIA-0196217."


JOINT RENAMING TEMPLATE

Here's the joint renaming template that my unreleased Python script 
uses, with a variety of comments that come from my analysis of the skeleton.
The left column is the original joint name used by the CMU dataset,
and the right column is the joint name that my script outputs.  Most
of the time this right-column name is one that MotionBuilder
recognizes, however in some cases we have to intentionally convert to
a name that MotionBuilder won't recognize, because we don't want
MotionBuilder to use the joint when we characterize.

---------------------------------------------------------------------
# Some facts about the CMU skeleton:
# lhipjoint and rhipjoint are in the same location as hip, and have no
#   keyframes.
#
# lowerback is in the same location as hip, and has keyframes. MotionBuilder
# docs say that Spine must NOT be in same location as hip, so we have to
# throw out "lowerback" and not call it Spine.
#
# thorax, lowerneck, lclavicle, and rclavicle are all in the same location.
# thorax and lowerneck are keyed.  lclavicle and rclavicle are not.
#
# Although we have two neck joints, the CMU "lowerneck" is really in
# the middle of the spine -- it sure doesn't look anywhere close to
# the human neck to me.  However when I tried calling it Spine2,
# MB gave a warning: "Hierarchy warning: LeftShoulder is not the direct
# descendant of Spine2, Spine1 was found".
#
# Per CMU web page: 'The "finger" and "thumb" joints are added to the
# skeleton for editing convenience - we do not actually capture these
# joints' motions and any such data should be ignored.'

TEMPLATE: cmu
hip                                     Hips

# Not sure what to do with lhipjoint.  It has no keyframes and is
# just a connector to attach the leg, so probably OK to rename it
# in a way that MB won't use it.
 lhipjoint                              LHipJoint  # Not used by MB
  lfemur                                LeftUpLeg
   ltibia                               LeftLeg
    lfoot                               LeftFoot
     ltoes                              LeftToeBase
 rhipjoint                              RHipJoint
   rfemur                               RightUpLeg
    rtibia                              RightLeg
     rfoot                              RightFoot
      rtoes                             RightToeBase

# We can't translate "lowerback" to Spine because lowerback is in
# the same location as Hips.  The MB docs say that you shouldn't do
# that.
 lowerback                              LowerBack  # child of hips
  upperback                             Spine
   thorax                               Spine1

# "Lower" and "upper" neck?  Good grief.
    lowerneck                           Neck
     upperneck                          Neck1
      head                              Head
    lclavicle                           LeftShoulder    # child of
    thorax
     lhumerus                           LeftArm
      lradius                           LeftForeArm
       lwrist                           LeftHand
        lhand                           LeftFingerBase
# LFingers and LThumb aren't names used by MB.  CMU notes that there's
# no data on these joints, so we want to ignore them.
         lfingers                       LFingers
        lthumb                          LThumb  # child of lwrist
    rclavicle                           RightShoulder # child of thorax
     rhumerus                           RightArm
      rradius                           RightForeArm
       rwrist                           RightHand
        rhand                           RightFingerBase
         rfingers                       RFingers
        rthumb                          RThumb  # child of rwrist

# END OF CMU JOINT RENAMING TEMPLATE with comments
-----------------------------------------------------------------


CONTACT INFO AND WHERE TO FIND STUFF:
  This BVH conversion release: www.cgspeed.com in the motion capture section
  Original CMU database (not BVH): mocap.cs.cmu.edu
  AMC2BVH freeware utility: http://vipbase.net/amc2bvh/
  MotionBuilder: www.autodesk.com/motionbuilder
  BVHacker free BVH editing software: http://davedub.co.uk/bvhacker
    BVHacker is designed primarily to create BVH files for SecondLife.

To contact the creator of this BVH conversion release: hahne@io.com

If you like this BVH conversion release, feel free to drop me email
and let me know what you're doing with it.
