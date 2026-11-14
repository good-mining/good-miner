# Security

## Check your download

Every release lists a SHA-256 checksum for each file (`SHA256SUMS` and the release notes).

```text
Linux:    sha256sum -c SHA256SUMS
Windows:  Get-FileHash .\<file> -Algorithm SHA256
```

If the checksum does not match, do not run the file, and tell us. Download only from this repository's
Releases page or from good-miner.com.

## Antivirus warnings

Antivirus products flag most mining software, because mining malware exists. A flag on a file whose checksum
matches ours is a false positive; each release links its VirusTotal report so you can see who flags it.

## Report a vulnerability

Write to `security@good-miner.com` (active from the first release; until then, open an issue that says only
"security contact wanted" and we will reach you privately). Please do not post the details in public. We answer within three working
days and will credit you in the release that fixes it, if you wish.
