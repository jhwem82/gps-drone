------------------------------------------------------------------------------------------------------
 An open-source computational platform for outdoor navigation using a low-cost quadrotor 
------------------------------------------------------------------------------------------------------

Abstract: 
This paper reports the design and the experimental validation of a novel mechatronic solution, developed to support outdoor flights using an affordable commercial quadrotor and a personal computer as the basic hardware. The text discusses some technical details of the developed platform, making clear to the readers how to achieve real-time navigation capabilities adopting a simplified dynamic model as a high-level representation of the vehicle in flight, a general-purpose nonlinear controller, suitable for different types of control applications, and a sensor fusion algorithm, designed to compensate for delayed measurements in the available sensorial data. In order to check the effectiveness of the proposed algorithms, results associated to some experimental flights are presented, with the vehicle accomplishing positioning tasks, including waypoint navigation, and trajectory tracking tasks. Such results, in parallel to the theoretical analysis provided, allows claiming that the proposed platform is efficient under several scenarios. Additionally, the source code used is made freely available for download and modification, resulting in an open-source computational platform, valuable as a starting point for beginning researchers in the field of aerial robotics.
------------------------------------------------------------------------------------------------------
The codes of the open-source computational platform ... will be available after the article acceptance ...
Information about the basis code compilation can be found in https://github.com/puku0x/cvdrone
This code example was compiled using Windows 7 and Visual Studio 2010.
------------------------------------------------------------------------------------------------------
Important modifications over CVDrone:
  "command.cpp"
  1) Function Move3D:
      Change of the nomenclature of the high-level commands:
        cmd_vx <-> u_theta; 
        cmd_vy <-> -u_phi;
        cmd_vz <-> u_z
        cmd_vr <-> u_psi
      Exclude the internal function gains;
  2) Change the maximum values for the controller
      Set vz_max for 1 [m/s]: sockCommand.sendf("AT*CONFIG=%d,\"control:control_vz_max\",\"%d\"\r", ++seq, 1000);
      Set inc_max for 15 [°]: sockCommand.sendf("AT*CONFIG=%d,\"control:euler_angle_max\",\"%f\"\r", ++seq, 15.0 * DEG_TO_RAD);
      Set vr_max for 100 [°/s]: sockCommand.sendf("AT*CONFIG=%d,\"control:control_yaw\",\"%f\"\r", ++seq, 100.0 * DEG_TO_RAD);
      Set z_max for 10 [m]:  sockCommand.sendf("AT*CONFIG=%d,\"control:altitude_max\",\"%d\"\r", ++seq, 10000);
  
  "navdata.cpp"
  1) Disable bootstrap mode
      sockCommand.sendf("AT*CONFIG=%d,\"general:navdata_demo\",\"FALSE\"\r", ++seq);

Instalation guide:
Tutorial for keyboard control of the flight (from computers with Windows)
Tutorial for wi-fi range extension.

-----------------------------------------------------------------
 CV Drone (= OpenCV + AR.Drone)
 Copyright (C) 2016 puku0x
 https://github.com/puku0x/cvdrone
-----------------------------------------------------------------

INTRODUCTION
  CV Drone is free software; you can redistribute it and/or
  modify it under the terms of EITHER:
   (1) The GNU Lesser General Public License as published by the Free
       Software Foundation; either version 2.1 of the License, or (at
       your option) any later version. The text of the GNU Lesser
       General Public License is included with this library in the
       file cvdrone-license-LGPL.txt.
   (2) The BSD-style license that is included with this library in
       the file cvdrone-license-BSD.txt.

  This software is distributed in the hope that it will be useful,
  but WITHOUT ANY WARRANTY; without even the implied warranty of
  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the files
  cvdrone-license-LGPL.txt and cvdrone-license-BSD.txt for more details.

HOW TO INSTALL
  Please unzip "cvdrone-master.zip" into an arbitrary directory.

HOW TO UNINSTALL
  Please delete the cvdrone folder.

BEFORE YOU BUILD
  You should install Visual Studio before you build CV Drone.
  CV Drone supports VC++2010/2012/2013/2015.
  To download VS, please see http://www.microsoft.com/visualstudio/eng/downloads .

HOW TO USE
  1. Open \build\vs20xx\test.sln
  2. Press F7 to build.
  3. Press F5 (or Ctrl+F5) to run.
  4. You can play around with OpenCV. Sample codes are in "src\samples".

FOR AR.DRONE 1.0 USERS
  Please update your AR.Drone's firmware to 1.11.5.

FOR AR.DRONE 2.0 USERS
  Please update your AR.Drone's firmware to 2.4.8.

FOR VS2010 USERS
  You can not build CV Drone by VS2010 after you installed VS2012.
  To build VS2010, 
    1) You should install "Visual Studio 2010 SP1".  [Recommended]
    or,
    2) You should uninstall ".Net Framework 4.5" and re-install "4.0".

LIBRARY DEPENDENCIES
  CV Drone uses following libraries.
  - OpenCV 3.1.0 <3-clause BSD license>
    http://opencv.org/
  - FFmpeg 2.2.3 <LGPL v2.1 license>
    http://www.ffmpeg.org/
  - stdint.h/inttypes.h for Microsoft Visual Studio r26 <BSD license>
    https://code.google.com/p/msinttypes/
  - POSIX Threads for Win32 2.9.1 <LGPL v2.1 license>
    http://www.sourceware.org/pthreads-win32/

  Marker-based AR sample uses following libraries adding to the above.
  - GLUT for Win32 3.7.6
    http://user.xmission.com/~nate/glut.html
  - MarkerDetector
    https://github.com/MasteringOpenCV/code/tree/master/Chapter2_iPhoneAR/Example_MarkerBasedAR/Example_MarkerBasedAR

  License files for each library can be found in the 'licenses' folder.

Thank you.