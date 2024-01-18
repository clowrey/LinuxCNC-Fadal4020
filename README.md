**Fadal 4020 Conversion Parts**
  1. x3 ASD-B3-2023-E 2kW, 3.1 kHz Bandwith, 24-bit encoder, EtherCAT
  2. x3 ECM-B3M-EA1320RS1 2kW, Rated Torque: 9.55 (N-m), Maximum 28.65 (N-m)
  3. x1 VFD49AMH23ANSHA VFD-MH300, 15HP, 11kw, (HD 49A), 3 Ø 230VAC, 2000Hz
  4. x1 CMM-EC01 EtherCAT Communication Card
  5. x1 EMM-PG01L Encoder Module

**Useful Links**
* https://github.com/LinuxCNC/linuxcnc
* https://github.com/kcjengr/probe_basic/tree/main
* https://github.com/kcjengr/qtpyvcp
* https://github.com/persei802/QtDragon_hd/
* http://tom-itx.no-ip.biz:81/~webpage/cnc/configs/NEW_MILL_SHOP_2.8.4/ -- Axis config with side panel from Tom_L, one for A axis, one without
  
**Basic Install Steps**
1. Install linuxCNC which as of now is https://www.linuxcnc.org/iso/LinuxCNC_2.9.2-amd64.hybrid.iso from https://linuxcnc.org/downloads/
    * The default image from downloads is actually from RodW as of today 1/17/2024 and includes the repos for Probe Basic + EtherCAT https://forum.linuxcnc.org/9-installing-linuxcnc/49819-debian-12-bookworm-live-installer-iso-for-linuxcnc-x86-64

    If like me upon trying to update / upgrade you get errors about raspi-firmware then run these lines...[ as explained here](https://forum.linuxcnc.org/9-installing-linuxcnc/49819-debian-12-bookworm-live-installer-iso-for-linuxcnc-x86-64?start=110#290983)
    ```
    rm /etc/{initramfs/post-update.d/,kernel/{postinst.d/,postrm.d/}}z50-raspi-firmware
    apt purge raspi-firmware
    ```

3. Install EtherCAT https://forum.linuxcnc.org/ethercat/45336-ethercat-installation-from-repositories-how-to-step-by-step

    -- you dont need to run the hidden (spoiler) commands on that page
   
    -- you may have to create the dev directory in your home folder - I did not have one

    -- after ```sudo halcompile --install cia402.comp``` you should be able to move onto the next step of testing with the Delta B3 config from gchesney

4. Example Delta B3 config [https://github.com/gchesney/linuxcnc-asda-b3-e-configs](https://github.com/gchesney/linuxcnc-asda-b3-e-configs)

    * Adjust "setp cia402.0.pos-scale 10000000" in ethercat-test.hal to have some visible movement
    * Delta ASDA-Soft to disable the limits + emergency stop inputs if you desire 
        *P2.011 through 13 to disabled - otherwise you will always have the AL013 alarm - you should have Estop in a real machine
        *If running from a single phase supply during testing you will also have to disable some of the low voltage alarms..
    ![image](https://github.com/clowrey/LinuxCNC-Fadal4020/assets/6935928/08a85ce8-dc3d-488c-aabb-e7375cb46d4a)


**Setup Notes**

* XRDP works okay as remote desktop server
  * the user needs to be logged out locally to be able to login via RDP

* Delta files download: https://downloadcenter.deltaww.com/en-US/DownloadCenter?v=1&CID=06&itemID=060201&downloadID=B3%20Series&sort_expr=cdate&sort_dir=DESC
  *  Delta ASDA-Soft allows you to configure 1000s of settings and view very useful debugging information on the drives
  * I havent found out how to actually get the firmware update files - maybe they must be requested from Delta..

* The HAL Scope is cool!! Use the x-drv-act-velo to get some neat torque curves
![image](https://github.com/clowrey/LinuxCNC-Fadal4020/assets/6935928/b902c1cc-a7c7-462b-9e64-15960e74ded6)


* USB isolator to avoid encoder errors while configuring drive via USB, I assume from ground loops https://www.aliexpress.us/item/3256801182770545.html
  
  ![image](https://github.com/clowrey/LinuxCNC-Fadal4020/assets/6935928/0739d409-364d-4051-bb37-04512a0eb0d1)




