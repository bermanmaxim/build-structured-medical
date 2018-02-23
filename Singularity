Bootstrap: docker
From: jjanzic/docker-python3-opencv

%files
alucchi_cmake.patch /opt
FindOpenCV.cmake /opt

%post
apt-get install -y doxygen graphviz libboost-dev libboost-graph-dev libboost-program-options-dev
cd /opt
wget -qO- https://sourceforge.net/projects/itk/files/itk/4.7/InsightToolkit-4.7.2.tar.gz | tar -xzv
mv InsightToolkit-4.7.2 ITK && mkdir ITK/build
#
cd ITK/build
cmake -DModule_ITKReview:BOOL=ON ..
make -j8
cd /opt
#
git clone --depth 1 https://github.com/alucchi/structured_prediction_for_segmentation.git
#
cd structured_prediction_for_segmentation/lib/slic
cmake .; make
cd ../libDAI024
cmake .; make
cd /opt
#
patch structured_prediction_for_segmentation/CMakeLists_common.txt < alucchi_cmake.patch
mkdir structured_prediction_build; cd structured_prediction_build
cmake ../structured_prediction_for_segmentation
make -j8
#
# recursive grant permissions to /opt
chmod -R o=u /opt
# cleanup
rm -rf /var/lib/apt/lists/*





