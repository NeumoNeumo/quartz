---
id: print_stack
aliases: []
tags: []
---

## Common Sense

### Auto-Discovery

On linux, `avahi-daemon` is usually responsible for `mDNS/DNS-SD`. driverless, ippfind, lpinfo, cups-browsed can discover printer services through it. For example, `ippfind _ipp._tcp` sends a query for `_ipp._tcp.local.`. A printer may respond with `_ipp._tcp.local. PTR Brother MFC-9350CDW._ipp._tcp.local.`.

Another example:
```bash
~ ❯ sudo lpinfo -v
network lpd
network beh
network http
network socket
network https
network ipps
network ipp
network dnssd://Brother%20MFC-8540DN._ipp._tcp.local/?uuid=e3248000-80ce-11db-8000-b422009c5154
network dnssd://Brother%20MFC-9350CDW%20%5B3c2af48c185b%5D._ipp._tcp.local/?uuid=e3248000-80ce-11db-8000-3c2af48c185b
network ipp://Brother%20MFC-8540DN._ipp._tcp.local/
network ipp://Brother%20MFC-9350CDW%20%5B3c2af48c185b%5D._ipp._tcp.local/
```

> [!note]
> lpd, ips, etc., are different backends located under `/usr/lib/cups/backend`. In this example, both lpd and ips discovered services they can handle, so the same physical printer appears more then once.

> [!note]
> mDNS performs DNS queries using multicast groups when no DNS server is available, allowing devices to answer queries themselves. DNS-SD uses DNS for service discovery. It does not strictly require mDNS; it also works over ordinary unicast DNS. In DNS-SD, the special query `_services._dns-sd._udp.local.` is used to enumerate all advertised services.

### Traditional PPD config

A PPD, or PostScript Printer Description, is effectively a printer capability description file containing information such as
```text
paper sizes
DPI / resolution
built-in fonts
color capability
duplex support
hole punching support
finishing options
input trays
supported printer options
```

When a printer does not support a input format, a filter converts the document into a format the printer understands, like pdf to postscript. A traditional CUPS driver is PPD + filter. `Generic PostScript Printer` describes a conservative, generic PostScript printer rather than the exact capabilities of a specific device.

### Auto IPP config

With IPP, CUPS dynamically queries the printer’s capabilities from the printer itself. The options shown in a graphical print dialog are derived from these queried capabilities.

```bash
# Inspect the capabilities
ipptool -tv ipp://[printer-ip]/ipp/print get-printer-attributes.test
# View the PPD generated from IPP attributes
driverless ipp://[printer-ip]/ipp/print
```

`lpadmin` creates persistent queue, whose config stored under `/etc/cups`. CUPS may create a temp queue for printers supporting IPP. This can happen when using `lp -d Brother_MFC_9350CDW_3c2af48c185b -o sides=two-sided-long-edge document.pdf`.

### Call Stack

A typical CUPS print path looks like this:
```text
lp / lpr
  ↓
libcups
  ↓
cupsd
  ↓
printer queue lookup
  ↓
PPD or IPP capability lookup
  ↓
MIME type detection
  ↓
filter chain selection
  ↓
format conversion: e.g. pdf 2 postscript/PCL/raster
  ↓
backend: ipp / ipps / socket / lpd / usb
  ↓
printer
```

By contrast, `ipptool` bypasses `cupsd` and communicates directly with the printer using IPP, like `ippfind _ipp._tcp --exec ipptool -tv -f document.pdf '{}' print-job.test \;`

> [!note]
> Use this command carefully: if multiple printers advertise _ipp._tcp, all of them may receive the print job.

`ipptool` is useful for debugging, but it neither auto choose a CUPS filter chain nor maintain default print settings. `lp` is better for everyday printing.

Both `cupsd`-related tools and `ipptool` are linked against `libcups.so`.

## Common Commands

```bash
# Show available printers
lpstat -e
# Set a default printer
lpoptions -d Brother_MFC_9350CDW_3c2af48c185b
# Show supported options
lpoptions -p  -l
# Default config stored in `~/.cups/lpoptions`
lpoptions -p Brother_MFC_9350CDW_3c2af48c185b -o sides=two-sided-long-edge
# Print doc.pdf with duplex enabled
lp -d Brother_MFC_9350CDW_3c2af48c185b -o sides=two-sided-long-edge doc.pdf
# Show jobs in the queue
lpq -al
# Show completed/incomplete jobs
lpstat -W completed
lpstat -W not-completed
# Cancel a job
lprm <job id>
```

If the output is garbled
```bash
pdffonts your_file.pdf
gs -o fixed_output.pdf -dNoOutputFonts -sDEVICE=pdfwrite input.pdf
```
