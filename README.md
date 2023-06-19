# Some helpful Linux tips

## Find the biggest subdirectories
    du -hs * | sort -rh | head -5

## Convert PDF to CBZ
    for DATEI in *.pdf; do
       DIR=$(mktemp -d)
       echo "Konvertiere ${DATEI}"
       pdftoppm -jpeg "${DATEI}" "${DIR}/IMAGE"
       ls -l "${DIR}"
       (cd ${DIR} && zip -FSr "${DATEI%.*}.cbz" *)
       mv "${DIR}/${DATEI%.*}.cbz" .
       rm -r "${DIR}"
    done


## Convert CBR to CBZ
    WORKDIR=$(pwd)
    find . -maxdepth 1 -name '*.cbr' -print0 | while read -d $'\0' CBR; do
    	echo "Read CBR  ${CBR}"
    	TEMPDIR=$(mktemp -d)
    	cd "${TEMPDIR}"
    	unrar e -inul "${WORKDIR}/${CBR}"

    	CBZ="${CBR%.cbr}.cbz"
    	echo "Write CBZ ${CBZ}"
    	zip -q "${WORKDIR}/${CBZ}" *

    	cd "${WORKDIR}"
    	rm "${CBR}"
    	rm -r "${TEMPDIR}"
    done


## Convert HEIC to JPG

    for bild in $(ls *.heic); do 
    	echo $bild
    	./tifig -i $bild -v -q 100 ${bild/%.heic/.jpg}
    	rm $bild
    done;
