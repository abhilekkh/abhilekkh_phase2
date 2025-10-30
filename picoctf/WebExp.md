
 
# 1. Trivial Flag Transfer Protocol  

> Figure out how they moved the flag.

## Solution:

- Accessed the web application and the filter.php page which shows filtered keywords for each round. 
- Round 1 had filter 'or' so I used the SQL comment -- to bypass the password check. Payload: admin' --
- Round 2 had filters 'or', 'and', 'like', '=', '--' so the -- comment was blocked hence I used the alternative SQLite comment '/*'. Payload: admin' /*
- Round 3 had filters  'or', 'and', 'like', '=', '--','>','<' hence used the semicolon ; to terminate the SQL statement before the password check. Payload: admin';
- Round 4 had filters 'or', 'and', 'like', '=', '--', '>', '<', 'admin'now the keyword admin was blocked so used SQLite's string concatenation operator || to construct 'admin'. Payload: ad'||'min';
- Round 5 had filters 'or', 'and', 'like','=', '--', '>', '<', 'admin', 'union' The concatenation payload from Round 4 still worked. Payload: ad'||'min';
- After completing Round 5, the flag was displayed


## Flag:

```
picoCTF{y0u_m4d3_1t_79a0ddc6}
```

## Concepts learnt:

- SQL injection techniques for bypassing authentication


## Resources:

- [Web Application Pentesting](./https://youtube.com/playlist?list=PLLKT__MCUeixCoi2jtP2Jj8nZzM4MOzBL)

***


# 2. SSTI1
> I made a cool website where you can announce whatever you want! Try it out!

Additional details will be available after launching your challenge instance.
## Solution:

- launched the instance, viewed the website, it announced anything which was written in it.
- hint suggested Server Side Template Injection, searched about it on google and found about different templates engines like jinja2.
- searched ssti flowchart to get the template engine being used which is jinja2 and then search jinja2 ssti payloads and found a payload that can run commands: {{ self._TemplateReference__context.cycler.__init__.__globals__.os.popen('ls').read() }}
- the website ran the ls command on its server and showed me the list of files: app.py, requirements.txt, and flag.
- saw the flag file,tpicoCTF{3v3ry1_l0v3s_c00k135_cc9110ba}o read it, I just modified my payload to use the cat command in place of ls {{ self._TemplateReference__context.cycler.__init__.__globals__.os.popen('cat flag').read() }}.
- so the flag was visible now

## Flag:

```
picoCTF{s4rv3r_s1d3_t3mp14t3_1nj3ct10n5_4r3_c001_bdc95c1a}
```

## Concepts learnt:

- learnt about ssti mainly jinja2 commands


## Resources:

- [SSTI](./https://medium.com/@bdemir/a-pentesters-guide-to-server-side-template-injection-ssti-c5e3998eae68)
- [SSTI FLowchart](./https://cdn.prod.website-files.com/6225a414ab1e86e4cd4c71d0/62750a98cf16788403fc63d5_SSTI%2520Flow%2520Chart.png)
***


# 3. Cookies
> Who doesn't love cookies? Try to figure out the best one. http://mercury.picoctf.net:64944/
## Solution:

- opened the webpage, tried writing random words but showed error, tried the sample word 'snickerdoodle' so it displayed I love snickerdoodle cookies
- since the challenge was named cookie I opened the cookies in inspect of webpage, in cookies found name with value =-1 initially but 0 when i entered snickerdoodle
- after changing value of name to 1 it showed I love chocolate chip cookies so now tried random values 100-> error, 50-> error then 25 it showed I love lebkuchen cookies now tried 30-> error, then 29-> error at 28 it gave I love white chocolate macadamia cookies
- now from 28 to 18 i tried all values and at 18 it gave the flag
## Flag:

```
picoCTF{3v3ry1_l0v3s_c00k135_cc9110ba}
```

## Concepts learnt:

- how to edit cookies

## Resources:

***
