# Chrome Obfuscated

- All functions we could uncover are being obfuscated here (95% of the binary)

Chrome is one of the most complex pieces of modern software, integrating an extensive array of libraries and technologies. It includes components such as OpenSSL for secure communications, HTTP parsers for web protocol handling, JSON parsers for data interchange, and the V8 JavaScript engine with its Just-In-Time (JIT) compiler for executing scripts at high speed. Additional components span networking, multimedia processing, rendering engines, sandboxing for security, and more, showcasing its incredible breadth as a cutting-edge web browser.

Being able to obfuscate the core component of chrome (chrome.dll) without breaking it is extremely impressive. We have included our obfuscated version of chrome.dll as well as the original in this repo.

- `win64-121.0.6167.85\chrome-win64\chrome.dll` - obfuscated
- `win64-121.0.6167.85\chrome-win64\chrome_original.dll` - non-obfuscated