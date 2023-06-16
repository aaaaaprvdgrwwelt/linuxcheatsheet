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


Made with https://stackedit.io/app
