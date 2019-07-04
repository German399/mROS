# mROS

A lightweight runtime environment of ROS1 nodes onto embedded systems

## Current Platform (embedded board)

- Renesas GR-PEACH

## How to get

- $ git clone --recursive https://github.com/tlk-emb/mROS

## Development Platform and Tools for Host PC

- IDE: [Atollic TrueSTUDIO](https://atollic.com/truestudio/)
  - Windows 10 Pro
  - Ubuntu 16.04.5
    - Currently we tested v.8.0.0, v.9.0.1 and v.9.1.0
- CUI
  - macOS High Sierra 10.13.6 / arm-none-eabi version 5.4.1 20160609 (Launchpad distribution)
  - Ubuntu 16.04 LTS / gcc-arm-none-eabi version 4.9.3 20150529 (apt package)
    - $ sudo apt install gcc-arm-none-eabi
  - Ubuntu 14.04.5 LTS / gcc-arm-none-eabi version 4.9.3 20150529 ([Launchpad distribution](https://launchpad.net/gcc-arm-embedded/4.9/4.9-2015-q3-update))

Please let us know if you could develop and build anothoer host OS.

## SW Components

- [asp-gr_peach_gcc-mbed](https://github.com/tlk-emb/asp-gr_peach_gcc-mbed)
  - Open-source Software Platform Based on TOPPERS/ASP Kernel, mbed and Arduino Library for Renesas GR-PEACH.
  - located at `asp_mbed/asp-gr_peach_gcc-mbed` as gitsubmodule
- [opencv-lib](https://github.com/d-kato/opencv-lib.git)
  - located at `opencv-lib` as gitsubmodule
- [TOPPERS configurator](http://toppers.jp/cfg-download.html)
  - located at `asp_mbed/cfg_binary`
  - (for Win) cfg-mingw-static-1_9_6.zip
  - (for Linux) cfg-linux-static-1_9_6.gz
    - $ sudo apt install libstdc++6 lib32stdc++6
  - (for macOS) cfg-osx-static-1_9_5.gz

## Build (v1.1)
- For CUI (terminal) (v1.1)
  - cd to project dir such as `workspace/app/`
  - Describe `USE_TRUESTUDIO = false` or comment-out such as `#USE_TRUESTUDIO = true` on Makefile
  - Edit `mros-lib/mros_msg-gen/including_msgs.json` and
    - Specify your catkin workspace such as `"catkin_ws_dir": "../../../catkin_ws/"`
    - Specify headers for message types that are used in your app such as 
    ```
    "including_msgs": [
      "mros_test/PersonalData.h",
      "std_msgs/String.h"
    ]
    ```
    - Specify depending packages for message types such as 
    ```
    "depending_packages": [
      "std_msgs",
      "mros_test"
    ]
    ```
  - Build ROS applications (= run catkin_make) to generate message type header files for ROS system
  - run `$ python (mROS root directory)/mros-lib/mros_msg-gen/mros_msg-gen.py` to generate message type header files for mROS applications
  - run `$ make clean && make` or `$ make depend && make`

## Build (v1.0)

- For TrueSTUDIO
  - Specify and open `workspace` as workspace
  - Import `workspace/*` such as `camera_app/`
    - Currently `app/` cannot be built
  - Describe `USE_TRUESTUDIO = true` on Makefile
  - You can bulid and debug the project
- For CUI (terminal)
  - cd to project dir such as `workspace/asp_sample1/`
  - Describe `USE_TRUESTUDIO = false` or comment-out such as `#USE_TRUESTUDIO = true` on Makefile
  - `$ make` or `$ make depend && make`



## TODO

- Describe how to use manual
- Support `MessageType`

## References

- Research papers
  - [Work-in-Progress: Design Concept of a Lightweight Runtime Environment for Robot Software Components Onto Embedded Devices
](https://ieeexplore.ieee.org/document/8537199)
    - Authors: Hideki Takase, Tomoya Mori, Kazuyoshi Takagi and Naofumi Takagi
    - 2018 International Conference on Embedded Software (EMSOFT), pp. 1-3, Turin, Italy, Sep 2018.
    - doi: 10.1109/EMSOFT.2018.8537199
  - mROS: A Lightweight Runtime Environment for Robot Software Components onto Embedded Devices
    - Authors: Hideki Takase, Tomoya Mori, Kazuyoshi Takagi and Naofumi Takagi
    - The 10th International Symposium on Highly-Efficient Accelerators and Reconfigurable Technologies (HEART 2019), Nagasaki, Jun 2019.
    - It will be appeared on ACM Portal

- Qiita article (in Japanese)
  - https://qiita.com/takasehideki/items/7d783ecd605dcee29ee0

