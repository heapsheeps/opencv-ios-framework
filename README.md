This repo stores a pre-built iOS framework for OpenCV.
The current version built is 4.11.0

Before cloning this repo, make sure to install git-lfs (`git lfs install`), since the framework is pushed as an LFS file.

--

To build a new version:
- `git submodule update --init` to init the opencv and contrib submodules
- cd to both the opencv AND opencv_contrib folders and checkout the version tag you need (e.g. `git checkout 4.11.0`)
- Create a python venv and `pip install jinja2` (Not sure if jinja2 is needed, but having `python` and not just `python3` on your path is required. Some scripts call it.)
- Run the python framework build helper:
```
python3 ./opencv/platforms/ios/build_framework.py \
  ./build \
  --contrib ./opencv_contrib \
  --iphoneos_deployment_target 13.0 \
  --iphoneos_archs arm64 \
  --iphonesimulator_archs x86_64 \
  --disable-swift # Errors building with swift bindings enabled ("missing swift compiler")

# other params (not used)
#  --debug # builds debug libraries
#  --enable_nonfree # if needed
```
- Copy the framework out of the build folder `cp -r ./build/opencv2.framework ./`
- Commit the new framework and push
