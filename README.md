<script>
    var url = 'https://github.com/ferenk/github-tests/releases/download/Web/download_stats.txt';
    var storedText;

    async function refreshStats()
    {
    fetch(url)
        .then(function(response) {
        response.text().then(function(text) {
        storedText = text;
        let prevLine = '';
        let downloadCount = 0;
        const textLines = text.split('\n');
            for (let i = 0; i< textLines.length; i++) {
            if (textLines[i].includes('download_count') && prevLine.includes('manifest.json')) {
                downloadCount += parseInt(textLines[i].split(':')[1].trim(', '));
                document.getElementById('downloadedCount').textContent = downloadCount;
            }
            prevLine = textLines[i];
            }
        });
    });
    }

    function done() {
    document.getElementById('log').textContent =
        "Here's what I got! \n" + storedText;
    }

    document.addEventListener('DOMContentLoaded', refreshStats);
</script>




Status:
[![.github/workflows/test.yml](https://github.com/ferenk/github-tests/actions/workflows/test.yml/badge.svg)](https://github.com/ferenk/github-tests/actions/workflows/test.yml)

Downloaded: <span id="downloadedCount"></span>
