List of disposable email domains
========================

This repo contains a list of disposable and temporary email address domains often used to register dummy users in order to spam or abuse some services.

We cannot guarantee all of these can still be considered disposable but we do basic checking so chances are they were disposable at one point in time.



Example Usage
=============

#### Python :

```Python
blocklist = ('temporary-email-domains.conf')
blocklist_content = [line.rstrip() for line in blocklist.readlines()]
if email.split('@')[1] in blocklist_content:
    message = "Please enter your permanent email address."
    return (False, message)
else:
    return True
```

#### NodeJs :

```javascript
'use strict';

const readline = require('readline'),
  fs = require('fs');

const input = fs.createReadStream('./temporary-email-domains.conf'),
  output = [],
  rl = readline.createInterface({input});

// PROCESS LINES
rl.on('line', (line) => {
  console.log(`Processing line ${output.length}`);
  output.push(line);
});

// SAVE AS JSON
rl.on('close', () => {
  try {
    const json = JSON.stringify(output);
    fs.writeFile('disposable-email-blocklist.json', json, () => console.log('--- FINISHED ---'));
  } catch (e) {
    console.log(e);
  }
});
```

#### C# :

```C#
private static readonly Lazy<HashSet<string>> _emailBlockList = new Lazy<HashSet<string>>(() =>
{
  var lines = File.ReadLines("temporary-email-domains.conf")
    .Where(line => !string.IsNullOrWhiteSpace(line) && !line.TrimStart().StartsWith("//"));
  return new HashSet<string>(lines, StringComparer.OrdinalIgnoreCase);
});

private static bool IsBlocklisted(string domain) => _emailBlockList.Value.Contains(domain);

...

var addr = new MailAddress(email);
if (IsBlocklisted(addr.Host)))
  throw new ApplicationException("Email is blocklisted.");
```
