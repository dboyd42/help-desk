dnsrecon
########
:Author: David Boyd
:Date: 2020-11-10

[ERROR] KeyError
****************
:Status: Solved
:Reason: WSL Kali's repo isn't updated to Github's version.
:Solution: Fix the code (line 846)

[ERROR] Output
==============
:Reason: KeyError exception is raised when you try to access a key that isn't in a dictionary

.. code-block:: Bash

	dnsrecon -d asterisk.org
		[*] Performing General Enumeration of Domain: asterisk.org
		[-] DNSSEC is not configured for asterisk.org
		[*]      SOA ns.digium.com 216.207.245.18
		[*]      NS nsx3.digium.com 166.78.177.30
		Traceback (most recent call last):
		File "./dnsrecon.py", line 1691, in <module>
		main()
		File "./dnsrecon.py", line 1651, in main
		std_enum_records = general_enum(res, domain, xfr, bing, yandex,
		spf_enum, do_whois, do_crt, zonewalk)
		File "./dnsrecon.py", line 934, in general_enum
		bind_ver = check_bindversion(res, ns_rcrd[2],
		res._res.timeout)
		File "./dnsrecon.py", line 847, in check_bindversion
		print_status(f"\t Bind Version for {ns_server}
		{response.answer[0].items[0].strings[0]}")
		KeyError: 0

[ERROR] dnsrecon.py Output
==========================

.. code-block:: Bash

	cat -n /usr/share/dnsrecon/dnsrecon.py | sed -n 836,854p
		836 def check_bindversion(res, ns_server, timeout):
		837     """
		838     Check if the version of Bind can be queried for.
		839     """
		840     version = ""
		841
		842     if not CONFIG or not CONFIG.get("disable_check_bindversion", False):
		843         request = dns.message.make_query('version.bind', 'txt', 'ch')
		844         try:
		845             response = res.query(request, ns_server, timeout=timeout, one_rr_per_rrset=True     )
		846             if len(response.answer) > 0:
		847                 print_status(f"\t Bind Version for {ns_server} {response.answer[0].items[0]     .strings[0]}")
		848                 version = response.answer[0].items[0].strings[0]
		849         except (dns.resolver.NXDOMAIN, dns.exception.Timeout, dns.resolver.NoAnswer, socket     .error,
		850                 dns.query.BadResponse):
		851             pass
		852
		853     return version
		854

[SOLUTION] dnsrecon.py
======================
:Reference URL: `DNSRecon <https://github.com/darkoperator/dnsrecon/blob/master/dnsrecon.py>`_

On line 846, modify if statement to include 'items' in dictionary.

.. code-block:: Bash

	# Open dnsrecon as root for editing
	sudo vim /usr/share/dnsrecon/dnsrecon.py

.. code-block:: Python3

	# Amend line 846 to prevent KeyError exception
	846 | if len(response.answer) > 0 and 'items' in response.answer[0]:

[SOLUTION] Output
=================

Verify program functionality.

.. code-block:: Bash

	dnsrecon -d asterisk.org
		[*] Performing General Enumeration of Domain: asterisk.org
		[-] DNSSEC is not configured for asterisk.org
		[*]      SOA ns.digium.com 216.207.245.18
		[*]      NS nsx3.digium.com 166.78.177.30
		[*]      NS nsx1.digium.com 216.207.245.18
		[*]      NS nsx2.digium.com 216.207.245.19
		[*]      MX mail.digium.com 216.207.245.2
		[*]      A asterisk.org 35.221.39.253
		[*]      TXT asterisk.org v=spf1 a ip4:216.207.245.0/26 ip4:173.227.23.0/26 ~all
		[*] Enumerating SRV Records
		[+]      SRV _sip._udp.asterisk.org sip.asterisk.org 204.91.156.60 5060
		[+] 1 Records Found

