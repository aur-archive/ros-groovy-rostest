pkgdesc="ROS - Integration test suite based on roslaunch that is compatible with xUnit frameworks."
url='http://www.ros.org/'

pkgname='ros-groovy-rostest'
pkgver='1.9.50'
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')
makedepends=('ros-build-tools')

depends=(ros-groovy-rosunit
  ros-groovy-rospy
  ros-groovy-catkin
  ros-groovy-roslaunch
  boost)

build() {
  [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
  if [ -d ${srcdir}/rostest ]; then
    cd ${srcdir}/rostest
    git fetch origin --tags
    git reset --hard release/groovy/rostest/${pkgver}-0
  else
    git clone -b release/groovy/rostest/${pkgver}-0 git://github.com/ros-gbp/ros_comm-release.git ${srcdir}/rostest
  fi
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/rostest
  cmake ${srcdir}/rostest -DCATKIN_BUILD_BINARY_PACKAGE=ON -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
