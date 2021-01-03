.PHONY: vendor

DIST=${PWD}/dist

clean:
	rm -rf ${DIST} *.deb

install-dep-mac: 
	brew install libheif libexif libjpeg-turbo libpng glib gobject-introspection expat fftw orc little-cms2 libde265 

build-mac: clean
	mkdir -p ${DIST}/usr/local
	cd ../; CC=clang CXX=clang++ ./configure --prefix=${DIST}/usr/local --without-gsf  --without-magick  --without-OpenEXR --without-nifti --without-pdfium  --without-poppler --without-rsvg --without-openslide --without-matio  --without-cfitsio --without-libwebp --without-pangoft2 --without-tiff --without-giflib --without-imagequant; make; make install

install-dep-pi: 
	sudo apt install -y libexif12 libjpeg62-turbo libpng16-16 libglib2.0-dev libexpat1 libfftw3-bin liblcms2-2 libde265-0 libffi6 libpcre3
	#
	# 2. install libheif (osx brew) or build by itself (pi)

build-pi: clean
	mkdir -p ${DIST}/usr/local
	cd ../; ./configure --prefix=${DIST}/usr/local --without-gsf  --without-magick  --without-OpenEXR --without-nifti --without-pdfium  --without-poppler --without-rsvg --without-openslide --without-matio  --without-cfitsio --without-libwebp --without-pangoft2 --without-tiff --without-giflib --without-imagequant; make; make install

install-dep-linux: 
	sudo apt install -y libexif12 libjpeg-dev libpng16-16 libglib2.0-dev libexpat1 libfftw3-bin liblcms2-2 libde265-0 libffi7 libpcre3 libheif-dev gobject-introspection gir1.2-vips-8.0 libwebp-dev libwebp6, libwebpmux3, libwebpdemux2 libtiff-dev

build-linux: clean
	mkdir -p ${DIST}/usr
	cd ../; ./configure --prefix=${DIST}/usr --without-gsf  --without-magick  --without-OpenEXR --without-nifti --without-pdfium  --without-poppler --without-rsvg --without-openslide --without-matio  --without-cfitsio --without-pangoft2 --without-imagequant --with-libheif --with-libwebp --with-tiff --with-giflib --with-png --with-jpeg; make; make install

release-linux-amd64:
	cp -r linux-amd64/DEBIAN ${DIST}
	dpkg-deb --build dist
	mv dist.deb lomo-vips-linux-amd64.deb

release-linux-armhf:
	cp -r linux-armhf/DEBIAN ${DIST}
	cp /usr/local/lib/libheif* ${DIST}/usr/local/lib/
	dpkg-deb --build dist
	mv dist.deb lomo-vips-linux-armhf.deb
