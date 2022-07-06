These are the binaries for https://github.com/sopov/resumeio2pdf

I do not provide support for these files, if they do not work, then try to download the source files and build them yourself.

The files are provided without warranty as is (use at your own risk).

```bash
docker run --rm -it -v $PWD:/app -w /resumeio2pdf golang:1.18-alpine sh -c '
apk add git build-base
git clone https://github.com/sopov/resumeio2pdf .
BASE=/app
APP="resumeio2pdf"
for DIST in $(go tool dist list)
do
    GOOS="${DIST%/*}"
    GOARCH="${DIST#*/}"
    DIR="$BASE/$GOOS"
    FILE="$APP-$GOARCH"
    if [ $GOOS == "darwin" ]
    then
         DIR="$BASE/macos"
    fi
    if [ $GOOS = "windows" ]
    then
         FILE="${FILE}.exe"
    fi

    mkdir -p $DIR
    export GOOS GOARCH
    go build -v -o "$DIR/$FILE"
done
'
```
