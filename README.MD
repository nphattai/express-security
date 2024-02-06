## CSRF (Cross-Site Request Forgery):

# Use Anti-CSRF Tokens:

Implement anti-CSRF tokens in your web forms. Libraries like csurf for Express can help you generate and validate these tokens.
Example using csurf:

const csurf = require('csurf');
const csrfProtection = csurf({ cookie: true });

app.use(csrfProtection);

app.get('/myform', (req, res) => {
// Use csrfToken in your form
res.render('myform', { csrfToken: req.csrfToken() });
});

# SameSite Cookies:

Set the SameSite attribute for cookies to mitigate CSRF attacks.

app.use(session({
secret: 'your-secret-key',
cookie: { sameSite: 'strict' },
}));

## XSS (Cross-Site Scripting):

# Content Security Policy (CSP):

Implement a Content Security Policy to control which resources can be loaded on your page.

app.use((req, res, next) => {
res.setHeader('Content-Security-Policy', 'script-src \'self\'');
next();
});

# HTML Encoding:

Sanitize user input and encode it properly before rendering it on the page. Libraries like he can be useful for HTML encoding.

const he = require('he');

const userInput = '<script>alert("XSS attack")</script>';
const encodedInput = he.encode(userInput);

# Helmet Middleware:

Use the helmet middleware to set various HTTP headers, including XSS protection headers.

const helmet = require('helmet');
app.use(helmet());

# Use Template Engines Safely:

If you're using template engines, ensure they automatically escape content by default. For example, in EJS:

<%- userContent %>
