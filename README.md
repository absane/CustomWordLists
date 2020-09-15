# Wordlists

## Custom Quick Hits

    urls=("https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/Logins.fuzz.txt" \
        "https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/Common-DB-Backups.txt" \
        "https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/Common-PHP-Filenames.txt" \
        "https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/CommonBackdoors-ASP.fuzz.txt" \
        "https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/CommonBackdoors-JSP.fuzz.txt" \
        "https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/CommonBackdoors-PHP.fuzz.txt" \
        "https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/CommonBackdoors-PL.fuzz.txt" \
        "https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/Passwords.fuzz.txt" \
        "https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/quickhits.txt" \
        "https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/reverse-proxy-inconsistencies.txt" \
        "https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/Randomfiles.fuzz.txt" \
        "https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/RobotsDisallowed-Top1000.txt" \
        "https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/UnixDotfiles.fuzz.txt" \
        "https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/Vignette.fuzz.txt" \
        "https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/common-api-endpoints-mazen160.txt" \
        )

    tempFile=$(mktemp)

    # CGI 
    curl -s "https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/CGI-XPlatform.fuzz.txt" | sed "s|^|/|g" | awk '{print "scripts"$1"\nbin"$1"\ncgi"$1"\ncgi-bin"$1"\nnph-cgi"$1}' >> ${tempFile}

    for url in "${urls[@]}"; do
        wget "$url" -O - >> ${tempFile}
    done

    cat ${tempFile} | grep -v "^#" | sed "s|^/||g" | sed "s|^|/|g" | sort -u > custom-quickhits.txt

XXXX