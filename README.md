**Fadal 4020 Conversion Parts**
  1. ASD-B3-2023-E x3
  2. ECM-B3M-EA1320RS1 x3
  3. VFD49AMH23ANSHA x1
  4. CMM-EC01 x1
  5. EMM-PG01L x1

**Setup Notes**

* Delta files download: https://downloadcenter.deltaww.com/en-US/DownloadCenter?v=1&CID=06&itemID=060201&downloadID=B3%20Series&sort_expr=cdate&sort_dir=DESC
  *  Delta ASDA-Soft allows you to configure 1000s of settings and view very useful debugging information on the drives
  * I havent found out how to actually get the firmware update files - maybe they must be requested from Delta..

* Example Delta B3 config [https://github.com/gchesney/linuxcnc-asda-b3-e-configs](https://github.com/gchesney/linuxcnc-asda-b3-e-configs)

  * Adjust "setp cia402.0.pos-scale 10000000" in ethercat-test.hal to have some visible movement

* USB isolator to avoid encoder errors while configuring drive via USB, I assume from ground loops https://www.aliexpress.us/item/3256801182770545.html
  
  ![image](https://github.com/clowrey/LinuxCNC-Fadal4020/assets/6935928/0739d409-364d-4051-bb37-04512a0eb0d1)

* 

