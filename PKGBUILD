pkgdesc="ROS - This package provides a recovery behavior for the navigation stack that attempts to clear space by reverting the costmaps used by the navigation stack to the static map outside of a given area."
url='https://wiki.ros.org/clear_costmap_recovery'

pkgname='ros-noetic-clear-costmap-recovery'
pkgver='1.17.3'
arch=('i686' 'x86_64' 'aarch64' 'armv7h' 'armv6h')
pkgrel=1
license=('BSD')

ros_makedepends=(ros-noetic-catkin
  ros-noetic-cmake-modules
  ros-noetic-costmap-2d
  ros-noetic-nav-core
  ros-noetic-pluginlib
  ros-noetic-roscpp
  ros-noetic-tf2-ros)
makedepends=('cmake' 'ros-build-tools' 'eigen'
  ${ros_makedepends[@]})

ros_depends=(ros-noetic-costmap-2d
  ros-noetic-nav-core
  ros-noetic-pluginlib
  ros-noetic-roscpp
  ros-noetic-tf)
depends=(${ros_depends[@]} 'eigen')

_dir="navigation-${pkgver}/clear_costmap_recovery"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros-planning/navigation/archive/${pkgver}.tar.gz")
sha256sums=('6500e427f868ea63801203715f41cbec4ed1bd1f9a29ae130a74b3776a7684f6')

build() {
  # Use ROS environment variables
  source /usr/share/ros-build-tools/clear-ros-env.sh
  [ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

  # Create build directory
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build

  # Build project
  cmake ${srcdir}/${_dir} \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
        -DPYTHON_EXECUTABLE=/usr/bin/python \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
