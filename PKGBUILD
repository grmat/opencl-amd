# Maintainer: grmat <grmat@sub.red>

pkgname=opencl-amd
pkgdesc="OpenCL userspace driver, AMD hybrid version"
pkgver=17.10.429170
pkgrel=1
arch=('x86_64')
url='http://www.amd.com'
license=('custom:AMD')
makedepends=('wget')
depends=('ocl-icd' 'libdrm-amd')
conflicts=('amdgpocl')

DLAGENTS='https::/usr/bin/wget --referer https://support.amd.com/en-us/kb-articles/Pages/AMDGPU-PRO-Driver-for-Linux-Release-Notes.aspx -N %u'

prefix='amdgpu-pro-'
major='17.10'
minor='429170'
shared="opt/amdgpu-pro/lib/x86_64-linux-gnu"

source=("https://www2.ati.com/drivers/linux/ubuntu/${prefix}${major}-${minor}.tar.xz")
sha256sums=('cb1ea7f9756f197a976138d2c00f239ae4ee43b839fbb1ea57f8770957d4afd6')

pkgver() {
	echo "${major}.${minor}"
}

package() {
	mkdir "${srcdir}/opencl"
	cd "${srcdir}/opencl"
	ar x "${srcdir}/${prefix}${major}-${minor}/opencl-amdgpu-pro-icd_${major}-${minor}_amd64.deb"
	tar xJf data.tar.xz

	mv "${srcdir}/opencl/etc" "${pkgdir}/"
	mkdir -p ${pkgdir}/usr/lib
	mv "${srcdir}/opencl/${shared}/libamdocl64.so" "${pkgdir}/usr/lib/"
	mv "${srcdir}/opencl/${shared}/libamdocl12cl64.so" "${pkgdir}/usr/lib/"

	rm -r "${srcdir}/opencl"
}

