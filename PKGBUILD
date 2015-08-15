# Maintainer: Felix Yan <felixonmars@gmail.com>
# Contributor: cuihao <cuihao dot leo at gmail dot com>
# Contributor: Guten <ywzhaifei@gmail.com> 

pkgname=goagent
pkgver=2.1.11
pkgrel=1
pkgdesc="A gae proxy forked from gappproxy/wallproxy"
arch=("i686" "x86_64")
url="http://goagent.googlecode.com"
license=("GPL2")
depends=('python2' 'python2-pyopenssl')
optdepends=(
  'python26: (AUR) upload GAE code using /opt/server/uploader.zip'
  'python2-gevent-beta: (AUR) enable gevent support'
)
conflicts=('python2-gevent<=0.99')
source=(
  "$pkgname.daemon"
  "$pkgname.service"
  "$pkgname-$pkgver.tar.gz::https://github.com/goagent/goagent/tarball/v$pkgver"
)
backup=('etc/goagent')
install='goagent.install'

build() {
  cd "$srcdir"
  
  rm -rf $pkgname
  mv goagent-goagent-* $pkgname
}

package() {
  cd "$srcdir/$pkgname"

  # python2 fix
  sed -i -re "1s/python2?/python2/" local/*.py
  chmod +x local/proxy.py

  mkdir -p "$pkgdir/opt/goagent"
  cp -r local server "$pkgdir/opt/goagent"
  
  # remove windows-only files
  rm -f "$pkgdir/opt/goagent/"*/*.{vbs,dll,exe,manifest,bat}

  # remove CA.crt CA.key for security issues
  rm -f "$pkgdir/opt/goagent/local/CA.crt" "$pkgdir/opt/goagent/local/CA.key"

  # config file
  install -Dm644 "${pkgdir}/opt/goagent/local/proxy.ini" "${pkgdir}/etc/goagent"
  ln -sf "/etc/goagent" "${pkgdir}/opt/goagent/local/proxy.ini"

  # rc.d daemon
  install -Dm755 "${srcdir}/goagent.daemon" "${pkgdir}/etc/rc.d/goagent"

  # systemd service
  install -Dm644 "${srcdir}/goagent.service" "${pkgdir}/usr/lib/systemd/system/goagent.service"
}

# vim:set ts=2 sw=2 et:
md5sums=('94e66bb9673157bc7fcfc2e7d01be389'
         'a0223e4e436a4d5cc17f76fc1fbbc140'
         '25e32bdc0828439c061fa7bf5af4741a')
md5sums=('94e66bb9673157bc7fcfc2e7d01be389'
         'a0223e4e436a4d5cc17f76fc1fbbc140'
         'b78ae6933540f194907a1496f3fa6cd8')
