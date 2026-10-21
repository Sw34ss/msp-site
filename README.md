# Small MSP website template

A plain HTML, CSS and one tiny JavaScript file. No build step, no frameworks, no outside requests.
It works on Cloudflare Pages and GitHub Pages.

## What is in the folder

| File | Purpose |
| --- | --- |
| index.html | Home page |
| services.html, plans.html, about.html | Main pages |
| support.html | How current clients get help |
| contact.html | Quote request form |
| thanks.html | Optional thank-you page for after the form is sent |
| privacy.html | Short privacy page (starting point, not legal advice) |
| 404.html | Not-found page (both hosts use it automatically) |
| style.css | All styling. Colors and fonts are at the top |
| site.js | Mobile menu toggle |
| assets/favicon.svg | Logo and browser icon. Replace with your own |
| robots.txt, sitemap.xml | Search engine files |
| _headers | Security headers for Cloudflare Pages (GitHub Pages ignores it) |
| .nojekyll | Tells GitHub Pages not to process the files |
| CNAME.example | Rename to CNAME for a custom domain on GitHub Pages |

## 1. Customize it

Search every file for the word `EDIT`. Each one marks something to change or confirm. Then replace these:

- `Mendoza Cyber Support` is your working business name (still under review).
- `cmwVision.com` appears in emails, canonical links, robots.txt and sitemap.xml.
- `Lodi, California` and `San Joaquin County` are the service area.

On Mac or Linux, you can replace in bulk (check the result afterwards):

    sed -i '' 's/cmwVision.com/YOURREALDOMAIN.com/g' *.html *.xml *.txt   # Mac
    sed -i 's/cmwVision.com/YOURREALDOMAIN.com/g' *.html *.xml *.txt      # Linux

Do not publish placeholder prices, example report numbers you do not intend to deliver, or services you do not offer. The plans page tiers are examples to match your own final tiers.

## 2. Preview it on your computer

    python3 -m http.server 8000

Then open http://localhost:8000

## 3. Set up the contact form

A static site cannot receive form posts by itself. Use a form service. The template is set up for Formspree-style endpoints:

1. Create a free account with a form service and create a form.
2. Replace `https://formspree.io/f/YOUR_FORM_ID` in contact.html with your endpoint.
3. If you use a different provider, also update the `form-action` part of the Content-Security-Policy in `_headers`.
4. In the provider's settings, set the thank-you redirect to `https://cmwVision.com/thanks.html` if it offers that option.
5. Send a test message and confirm it arrives. Free plans have limits, so check them.

The hidden `_gotcha` field is a spam trap used by some providers. Remove or rename it if yours uses a different one.

## 4. Publish

### Cloudflare Pages

1. Put the folder in a Git repository, or use direct upload.
2. Create a Pages project. Build command: none. Output directory: the folder root.
3. Add your custom domain in the project's settings. This is easiest if the domain's DNS is on Cloudflare.

### GitHub Pages

1. Put the files in a repository and push.
2. Settings > Pages > deploy from the main branch, root folder.
3. For a custom domain, rename `CNAME.example` to `CNAME` and put your domain inside. Then add the DNS records GitHub's documentation lists.
4. Turn on "Enforce HTTPS" once the certificate is issued.

### If your domain also runs Microsoft 365 email

Only add or change the website records (the root and `www` entries). Do not delete or edit the existing MX, TXT (SPF, verification), autodiscover and DKIM records, or email will break. Export or screenshot your DNS records before changing anything.

## Before you push to a public repository

GitHub Pages on a free account publishes from a public repository, and HTML comments are visible to anyone who views the page source. After you have handled every `EDIT` note, remove the leftover comments (run this inside the folder; it works on Mac and Linux):

    perl -0pi -e 's/[ \t]*<!--\s*EDIT.*?-->//gs' *.html

Two visible `EDIT` texts live in privacy.html (the form provider name and the last-updated date). Fix those by hand, since they are page text, not comments.

## 5. Before you announce it

- [ ] Business name is cleared and final
- [ ] Every `EDIT` handled and every `cmwVision.com` replaced
- [ ] Prices, plan contents and service list match what you really offer
- [ ] Contact form tested end to end
- [ ] Privacy page reviewed and still accurate
- [ ] Checked on a phone and in a desktop browser
- [ ] Google Business Profile and local SEO tasks (W4 in your plan) queued
