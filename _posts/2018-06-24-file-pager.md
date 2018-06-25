---
layout: post
title:  "file-pager"
date:   2018-06-24 18:29:59 -0700
---

I end up opening files in a terminal to browse their contents fairly often.
`pager` and `less` make quick work of local files but aren't immediately useful for text logs and other content served over http(s).
The following bash script can be used to open either a local file or URL in a pager by conditionally downloading the file into a temporary directory beforehand:

{% highlight bash %}
#!/usr/bin/env bash

set -euo pipefail

if [[ $# == 0 || $1 == "-h" || $1 == "--help" ]]; then
    echo "Usage: $0 file"
    exit 0
fi

file="$1"

if [[ $file =~ ^http(s)://? ]]; then
    temp_file=$(mktemp)
    wget --quiet "$file" --output-document "$temp_file"
    file=$temp_file
fi

if hash pager 2>/dev/null; then
    pager "$file"
else
    less "$file"
fi
{% endhighlight %}

This could easily be expanded to support other protocols e.g. `(s)ftp://`.
This script is also in [gist] form.

[gist]: https://gist.github.com/marczych/0f2c85fdf4fee4b698375e65f744bf4f
