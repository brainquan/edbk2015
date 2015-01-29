<bounce-category-patterns>
    /spam/ spam-related
    /junk mail/ spam-related
    /blacklist/ spam-related
    /blocked/ spam-related
    /\bU\.?C\.?E\.?\b/ spam-related
    /\bAdv(ertisements?)?\b/ spam-related
    /unsolicited/ spam-related
    /\b(open)?RBL\b/ spam-related
    /realtime blackhole/ spam-related
    /http:\/\/basic.wirehub.nl\/blackholes.html/ spam-related
    /\bvirus\b/ virus-related
    /message +content/ content-related
    /content +rejected/ content-related
    /quota/ quota-issues
    /limit exceeded/ quota-issues
    /mailbox +(is +)?full/ quota-issues
    /sender ((verify|verification) failed|could not be verified|address rejected|domain must exist)/ invalid-sender
    /unable to verify sender/ invalid-sender
    /requires valid sender domain/ invalid-sender
    /bad sender's system address/ invalid-sender
    /No MX for envelope sender domain/ invalid-sender
    /^[45]\.4\.4/ routing-errors
    /no mail hosts for domain/ invalid-sender
    /Your domain has no(t)? DNS\/MX entries/ invalid-sender
    /REQUESTED ACTION NOT TAKEN: DNS FAILURE/ invalid-sender
    /Domain of sender address/ invalid-sender
    /return MX does not exist/ invalid-sender
    /Invalid sender domain/ invalid-sender
    /Verification failed/ invalid-sender
    /\bstorage\b/ quota-issues
    /(user|mailbox|recipient|rcpt|local part|address|account|mail drop|ad(d?)ressee) (has|has been|is)? *(currently|temporarily +)?(disabled|expired|inactive|not activa
ted)/ inactive-mailbox
    /(conta|usu.rio) inativ(a|o)/ inactive-mailbox
    /Too many (bad|invalid|unknown|illegal|unavailable) (user|mailbox|recipient|rcpt|local part|address|account|mail drop|ad(d?)ressee)/ other
    /(No such|bad|invalid|unknown|illegal|unavailable) (local +)?(user|mailbox|recipient|rcpt|local part|address|account|mail drop|ad(d?)ressee)/ bad-mailbox
    /(user|mailbox|recipient|rcpt|local part|address|account|mail drop|ad(d?)ressee) +(\S+@\S+ +)?(not (a +)?valid|not known|not here|not found|does not exist|bad|inval
id|unknown|illegal|unavailable)/ bad-mailbox
    /\S+@\S+ +(is +)?(not (a +)?valid|not known|not here|not found|does not exist|bad|invalid|unknown|illegal|unavailable)/ bad-mailbox
    /no mailbox here by that name/ bad-mailbox
    /my badrcptto list/ bad-mailbox
    /not our customer/ bad-mailbox
    /no longer (valid|available)/ bad-mailbox
    /have a \S+ account/ bad-mailbox
    /\brelay(ing)?/ relaying-issues
    /domain (retired|bad|invalid|unknown|illegal|unavailable)/ bad-domain
    /domain no longer in use/ bad-domain
    /domain (\S+ +)?(is +)?obsolete/ bad-domain
    /denied/ policy-related
    /prohibit/ policy-related
    /rejected/ policy-related
    /refused/ policy-related
    /allowed/ policy-related
    /banned/ policy-related
    /policy/ policy-related
    /suspicious activity/ policy-related
    /bad sequence/ protocol-errors
    /syntax error/ protocol-errors
    /syntax error/ protocol-errors
    /\broute\b/ routing-errors
    /\bunroutable\b/ routing-errors
    /\bunrouteable\b/ routing-errors
    /Invalid 7bit DATA/ content-related
    /^2.\d+.\d+;/ success
    /^[45]\.1\.[1346];/ bad-mailbox
    /^[45]\.1\.2/ bad-domain
    /^[45]\.1\.[78];/ invalid-sender
    /^[45]\.2\.0;/ bad-mailbox
    /^[45]\.2\.1;/ inactive-mailbox
    /^[45]\.2\.2;/ quota-issues
    /^[45]\.3\.3;/ content-related
    /^[45]\.3\.5;/ bad-configuration
    /^[45]\.4\.1;/ no-answer-from-host
    /^[45]\.4\.2;/ bad-connection
    /^[45]\.4\.[36];/ routing-errors
    /^[45]\.4\.4/ routing-errors
    /^[45]\.4\.6/ routing-errors
    /^[45]\.4\.7;/ message-expired
    /^[45]\.5\.3;/ policy-related
    /^[45]\.5\.\d+;/ protocol-errors
    /^[45]\.6\.\d+;/ content-related
    /^[45]\.7\.[012];/ policy-related
    /^[45]\.7\.7;/ content-related
    // other    # catch-all
</bounce-category-patterns>
############################################################################
# END: BOUNCE RULES
############################################################################


############################################################################
# BEGIN: BACKOFF RULES
############################################################################

<smtp-pattern-list common-errors> 
  reply /generating high volumes of.* complaints from AOL/    mode=backoff 
  reply /Excessive unknown recipients - possible Open Relay/  mode=backoff 
  reply /^421 .* too many errors/                             mode=backoff 
  reply /blocked.*spamhaus/                                   mode=backoff 
  reply /451 Rejected/                                        mode=backoff 
</smtp-pattern-list>

<smtp-pattern-list blocking-errors>
    #
    # A QUEUE IN BACKOFF MODE WILL SEND MORE SLOWLY
    # To place a queue back into normal mode, a command similar
    # to one of the following will need to be run:
    # pmta set queue --mode=normal yahoo.com
    # or
    # pmta set queue --mode=normal yahoo.com/vmta1
    #
    # To use backoff mode, uncomment individual <domain> directives
    #
    #AOL Errors
    reply /421 .* SERVICE NOT AVAILABLE/ mode=backoff
    reply /generating high volumes of.* complaints from AOL/ mode=backoff
    reply /554 .*aol.com/ mode=backoff
    reply /421dynt1/ mode=backoff
    reply /HVU:B1/ mode=backoff
    reply /DNS:NR/ mode=backoff
    reply /RLY:NW/ mode=backoff
    reply /DYN:T1/ mode=backoff
    reply /RLY:BD/ mode=backoff
    reply /RLY:CH2/ mode=backoff
    #
    #Yahoo Errors
    reply /421 .* Please try again later/ mode=backoff
    reply /421 Message temporarily deferred/ mode=backoff
    reply /VS3-IP5 Excessive unknown recipients/ mode=backoff
    reply /VSS-IP Excessive unknown recipients/ mode=backoff
    #
    # The following 4 Yahoo errors may be very common
    # Using them may result in high use of backoff mode
    #
    reply /\[GL01\] Message from/ mode=backoff
    reply /\[TS01\] Messages from/ mode=backoff
    reply /\[TS02\] Messages from/ mode=backoff
    reply /\[TS03\] All messages from/ mode=backoff
    #
    #Hotmail Errors
    reply /exceeded the rate limit/ mode=backoff
    reply /exceeded the connection limit/ mode=backoff
    reply /Mail rejected by Windows Live Hotmail for policy reasons/ mode=backoff
    reply /mail.live.com\/mail\/troubleshooting.aspx/ mode=backoff
    #
    #Adelphia Errors
    reply /421 Message Rejected/ mode=backoff
    reply /Client host rejected/ mode=backoff
    reply /blocked using UCEProtect/ mode=backoff
    #
    #Road Runner Errors
    reply /Mail Refused/ mode=backoff
    reply /421 Exceeded allowable connection time/ mode=backoff
    reply /amIBlockedByRR/ mode=backoff
    reply /block-lookup/ mode=backoff
    reply /Too many concurrent connections from source IP/ mode=backoff
    #
    #General Errors
    reply /too many/ mode=normal
    reply /Exceeded allowable connection time/ mode=backoff
    reply /Connection rate limit exceeded/ mode=backoff
    reply /refused your connection/ mode=backoff
    reply /try again later/ mode=backoff
    reply /try later/ mode=backoff
    reply /550 RBL/ mode=backoff
    reply /TDC internal RBL/ mode=backoff
    reply /connection refused/ mode=backoff
    reply /please see www.spamhaus.org/ mode=backoff
    reply /Message Rejected/ mode=backoff
    reply /refused by antispam/ mode=backoff
    reply /Service not available/ mode=backoff
    reply /currently blocked/ mode=backoff
    reply /locally blacklisted/ mode=backoff
    reply /not currently accepting mail from your ip/ mode=backoff
    reply /421.*closing connection/ mode=backoff
    reply /421.*Lost connection/ mode=backoff
    reply /476 connections from your host are denied/ mode=backoff
    reply /421 Connection cannot be established/ mode=backoff
    reply /421 temporary envelope failure/ mode=backoff
    reply /421 4.4.2 Timeout while waiting for command/ mode=backoff
    reply /450 Requested action aborted/ mode=backoff
    reply /550 Access denied/ mode=backoff
    reply /exceeded the rate limit/ mode=backoff
    reply /421rlynw/ mode=backoff
    reply /permanently deferred/ mode=backoff
    reply /\d+\.\d+\.\d+\.\d+ blocked/ mode=backoff
    reply /www\.spamcop\.net\/bl\.shtml/ mode=backoff
    reply /generating high volumes of.* complaints from AOL/    mode=backoff 
    reply /Excessive unknown recipients - possible Open Relay/  mode=backoff 
    reply /^421 .* too many errors/                             mode=backoff 
    reply /blocked.*spamhaus/                                   mode=backoff 
    reply /451 Rejected/                                        mode=backoff 
</smtp-pattern-list>

############################################################################
# END: BACKOFF RULES
############################################################################
