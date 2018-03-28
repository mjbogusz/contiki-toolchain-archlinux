pkgname=gcc-msp430-bin
pkgver=4.7.2
pkgrel=1
pkgdesc="GNU toolchain for the TI MSP430 processor, precompiled binary version"
arch=('x86_64')
url="http://sourceforge.net/projects/mspgcc/"
license=('GPL')
depends=('elfutils' 'libmpc')
source=("https://github.com/alexkrontiris/Setup-Contiki-Toolchain-in-Arch-Linux/raw/master/mspgcc-4.7.2-compiled.tar.bz2")
sha1sums=('c3fb2a9b963a81097605b05c2c3a3bb95c2f8707')
options=(!strip !libtool staticlibs !emptydirs docs)

# Output of `msp430-gcc -print-search-dirs` (formatted):
# install:
# 	/usr/lib/gcc/msp430/4.7.2/
# programs:
# 	/usr/libexec/gcc/msp430/4.7.2/
# 	/usr/libexec/gcc/
# 	/usr/msp430/bin/msp430/4.7.2/
# 	/usr/msp430/bin/
# libraries:
# 	/usr/lib/gcc/msp430/4.7.2/
# 	/usr/lib/gcc/
# 	/usr/msp430/lib/msp430/4.7.2/
# 	/usr/msp430/lib/

package() {
	mkdir -p ${pkgdir}/usr/lib
	mkdir -p ${pkgdir}/usr/share/man
	cp -R msp430/bin ${pkgdir}/usr/
	# main 'include' is empty
	# 'lib' contains also 'libiberty.a', present in base-devel - skip it
	cp -R msp430/lib/gcc ${pkgdir}/usr/lib/
	cp -R msp430/libexec ${pkgdir}/usr/
	cp -R msp430/msp430 ${pkgdir}/usr/
	# 'share/info' and 'share/locale' contains files present in base-devel - skip them
	cp -R msp430/share/man/man1 ${pkgdir}/usr/share/man/
}
