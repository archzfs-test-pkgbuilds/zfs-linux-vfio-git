# Maintainer: Jesus Alvarez <jeezusjr at gmail dot com>
#
# This PKGBUILD was generated by the archzfs build scripts located at
#
# http://github.com/archzfs/archzfs
#
# ! WARNING !
#
# The archzfs packages are kernel modules, so these PKGBUILDS will only work with the kernel package they target. In this
# case, the archzfs-linux-vfio packages will only work with the default linux-vfio package! To have a single PKGBUILD target many
# kernels would make for a cluttered PKGBUILD!
#
# If you have a custom kernel, you will need to change things in the PKGBUILDS. If you would like to have AUR or archzfs repo
# packages for your favorite kernel package built using the archzfs build tools, submit a request in the Issue tracker on the
# archzfs github page.
#
pkgbase="zfs-linux-vfio-git"
pkgname=("zfs-linux-vfio-git" "zfs-linux-vfio-git-headers")

pkgver=2018.03.28.r3390.13a2ff272.4.15.12.1
pkgrel=1
makedepends=("linux-vfio-headers=4.15.12-1" "git" "spl-linux-vfio-git-headers")
arch=("x86_64")
url="http://zfsonlinux.org/"
source=("git+https://github.com/zfsonlinux/zfs.git")
sha256sums=("SKIP")
license=("CDDL")
depends=("kmod" "spl-linux-vfio-git" "zfs-utils-common-git>=2018.03.28.r3390.13a2ff272" "linux-vfio=4.15.12-1")

build() {
    cd "${srcdir}/zfs"
    ./autogen.sh
    ./configure --prefix=/usr --sysconfdir=/etc --sbindir=/usr/bin --libdir=/usr/lib \
                --datadir=/usr/share --includedir=/usr/include --with-udevdir=/lib/udev \
                --libexecdir=/usr/lib/zfs-0.7.7 --with-config=kernel \
                --with-linux=/usr/lib/modules/4.15.12-1-vfio/build \
                --with-linux-obj=/usr/lib/modules/4.15.12-1-vfio/build
    make
}

package_zfs-linux-vfio-git() {
    pkgdesc="Kernel modules for the Zettabyte File System."
    install=zfs.install
    provides=("zfs")
    groups=("archzfs-linux-vfio-git")
    conflicts=('zfs-linux-vfio')
    replaces=("zfs-git")
    cd "${srcdir}/zfs"
    make DESTDIR="${pkgdir}" install
    cp -r "${pkgdir}"/{lib,usr}
    rm -r "${pkgdir}"/lib
    # Remove src dir
    rm -r "${pkgdir}"/usr/src
}

package_zfs-linux-vfio-git-headers() {
    pkgdesc="Kernel headers for the Zettabyte File System."
    conflicts=('zfs-archiso-linux-headers' 'zfs-archiso-linux-git-headers' 'zfs-linux-hardened-headers' 'zfs-linux-hardened-git-headers' 'zfs-linux-lts-headers' 'zfs-linux-lts-git-headers' 'zfs-linux-headers' 'zfs-linux-git-headers' 'zfs-linux-vfio-headers'  'zfs-linux-zen-headers' 'zfs-linux-zen-git-headers' )
    cd "${srcdir}/zfs"
    make DESTDIR="${pkgdir}" install
    rm -r "${pkgdir}/lib"
    # Remove reference to ${srcdir}
    sed -i "s+${srcdir}++" ${pkgdir}/usr/src/zfs-*/4.15.12-1-vfio/Module.symvers
}
