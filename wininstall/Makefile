VERSION := 9.4.1
WIXEXTENSIONS := -ext WixUIExtension

all: ChezScheme32.msi ChezScheme64.msi

ChezScheme32.msi: product.32.wixobj examples.32.wixobj i3nt.32.wixobj ti3nt.32.wixobj
	cmd.exe /c light.bat -nologo $(WIXEXTENSIONS) product.32.wixobj examples.32.wixobj i3nt.32.wixobj ti3nt.32.wixobj -sice:ICE64 -out "$@"

ChezScheme64.msi: product.64.wixobj a6nt.64.wixobj examples.64.wixobj ta6nt.64.wixobj
	cmd.exe /c light.bat -nologo $(WIXEXTENSIONS) product.64.wixobj a6nt.64.wixobj examples.64.wixobj ta6nt.64.wixobj -sice:ICE64 -out "$@"

%.32.wixobj: %.wxs
	cmd.exe /c candle.bat -nologo -dVersion=$(VERSION) $(WIXEXTENSIONS) $< -out $@

%.64.wixobj: %.wxs
	cmd.exe /c candle.bat -arch x64 -nologo -dVersion=$(VERSION) $(WIXEXTENSIONS) $< -out $@

.PHONY: workareas
workareas:
	cd ..; ./configure -m=a6nt; $(MAKE) -C a6nt/c
	cd ..; ./configure -m=i3nt; $(MAKE) -C i3nt/c
	cd ..; ./configure -m=ta6nt; $(MAKE) -C ta6nt/c
	cd ..; ./configure -m=ti3nt; $(MAKE) -C ti3nt/c

.PHONY: clean
clean:
	-rm -f Chez\ Scheme.msi *.wixobj *.wixpdb
