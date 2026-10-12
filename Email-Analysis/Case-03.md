# Static PDF Analysis Notes

## Example PDF

<img width="805" height="837" alt="Screenshot From 2026-09-08 13-35-30" src="https://github.com/user-attachments/assets/3f113a77-a971-4b29-b0fb-1c5cfcca5eba" />


The main goal of this PDF is to get the user to click the embedded button.

### Analysis with VirusTotal

Analyzed the PDF's hash value using VirusTotal.

<img width="913" height="69" alt="Screenshot From 2026-09-08 13-39-14" src="https://github.com/user-attachments/assets/130e65bc-f162-4470-9661-186df2e4c8dc" />


A trojan classification is applicable.

<img width="1465" height="892" alt="Screenshot From 2026-09-08 13-40-47" src="https://github.com/user-attachments/assets/52935594-e5af-4cf7-9eed-5964ea160c1a" />


### Analysis with a PDF Parser

<img width="952" height="397" alt="Screenshot From 2026-09-08 13-54-33" src="https://github.com/user-attachments/assets/b307e802-c94e-404f-bacc-601fe142c416" />


- The link embedded in the PDF (behind the button) is shown directly in the tool's output, giving access to the URL without opening the file at all.
- The PDF parser takes a filepath and scans the file on disk, which is less prone to user error than manually opening the file.

## Second PDF Sample

The attacker makes the file content appear blurred, with a "download" button designed to manipulate the user into clicking it. Results are relatively similar to the first sample, but the techniques used by the attacker differ.

### pdfid

<img width="953" height="485" alt="Screenshot From 2026-09-08 14-06-46" src="https://github.com/user-attachments/assets/ddc0a4e7-2a8a-4fae-8710-e5f71d95a8ce" />


`pdfid` gives a high-level overview of the objects present in a PDF file.

The example above lists `JS` and `JavaScript` objects. These typically stand out and warrant further investigation, since they can potentially be used to steal user data, establish a connection to an attacker's server, or launch external programs on the victim's system.

Other notable object types:

- **`/OpenAction`** — can cause the PDF reader to automatically take an action when the file is opened.
- **`/Launch`** — similar to `/OpenAction`, can trigger execution when the file is opened.
- **`/EmbeddedFile`** — indicates an attacker could have embedded malware within the PDF's content.

### Extracting Embedded Content

Using a PDF parser, embedded files and scripts can be extracted for closer inspection.

<img width="256" height="122" alt="Screenshot From 2026-09-08 14-30-50" src="https://github.com/user-attachments/assets/468b0559-e05c-459f-897b-a6ba3cb5e39e" />


The extracted file references another `.doc` file.

<img width="561" height="141" alt="Screenshot From 2026-09-08 14-31-49" src="https://github.com/user-attachments/assets/d8006680-f9d6-4eb3-913c-d880d06c6c30" />


The extracted content included a JavaScript action. The file was also encoded, so it was decoded by piping the PDF parser's output to a file and reviewing the decoded version.
