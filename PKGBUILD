# Maintainer: grmat <grmat@sub.red>

pkgname=(opencl-amd vulkan-amd)
pkgbase=(hybrid-amd)
pkgver=17.10.429170
pkgrel=1
arch=('x86_64')
url='http://www.amd.com'
license=('custom:AMD')
makedepends=('wget')
depends=('libdrm-amd')
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

package_opencl-amd() {
  pkgdesc="OpenCL userspace driver, AMD hybrid version"
  provides=('opencl-driver')
  conflicts=('opencl-mesa')
  depends=('ocl-icd')
  optdepends=('opencl-headers: headers necessary for OpenCL development')

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

package_vulkan-amd() {
  pkgdesc="Vulkan userspace driver, AMD hybrid version"
  provides=('vulkan-driver')
  conflicts=('vulkan-radeon')
  depends=('vulkan-icd-loader')
  optdepends=('vulkan-devel: for Vulkan development')

  mkdir -p "${srcdir}/vulkan"
  cd "${srcdir}/vulkan"
  ar x "${srcdir}/${prefix}${major}-${minor}/vulkan-amdgpu-pro_${major}-${minor}_amd64.deb"
  tar xJf data.tar.xz

  cd "${srcdir}/vulkan/etc/vulkan/icd.d"
  sed -i "s|opt/amdgpu-pro/lib/x86_64-linux-gnu|usr/lib|g" amd_icd64.json
  mkdir -p ${pkgdir}/usr/share
  mv "${srcdir}/vulkan/etc/vulkan" "${pkgdir}/usr/share/"
  mkdir -p ${pkgdir}/usr/lib
  cp "${srcdir}/vulkan/${shared}/amdvlk64.so" "${pkgdir}/usr/lib/"
}
