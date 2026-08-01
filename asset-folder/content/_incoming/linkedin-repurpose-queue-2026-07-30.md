# LinkedIn Repurpose Queue - 2026-07-30

Rule for this queue:

- Do not generate a post package until both caption/body and image/carousel/GIF evidence have been analyzed.
- Captions should stay about 70% similar to the reference caption's structure and core content, then be paraphrased into Stanley's voice.
- Firecrawl local capture attempt returned `FIRECRAWL_CONFIG_MISSING`.
- Direct LinkedIn guest HTML capture succeeded for the full LinkedIn URLs using `tools/linkedin_public_post_capture.py`.
- Feedshare images were extracted with `tools/download_linkedin_feedshare_images.py`.
- Reject unrelated saved images before drafting. Keep only feedshare/carousel assets whose visible topic matches the caption/body. Ignore unrelated people-only/profile-style images, including the African ladies image.

Drive completed before this queue:

- `youre-overpaying-5x-on-half-your-claude-activity`
- Drive folder: https://drive.google.com/drive/folders/1vC6J-cARzGLYtYYokNcvIx7DHW3VFviB

## Queue

1. https://lnkd.in/p/dr-jRJ28
   - Status: blocked.
   - Tried: public web lookup, `Invoke-WebRequest`, and `curl -L`.
   - Result: `403 Forbidden` and no usable redirect/caption/image.
   - Needs: full LinkedIn URL, caption paste, or screenshot.

2. https://lnkd.in/p/dvzDygwk
   - Status: blocked.
   - Tried: public web lookup, `Invoke-WebRequest`, and `curl -L`.
   - Result: `403 Forbidden` and no usable redirect/caption/image.
   - Needs: full LinkedIn URL, caption paste, or screenshot.

3. https://www.linkedin.com/posts/mickaelaubard_out-of-the-loop-on-claude-heres-10-must-have-activity-7487812971096825858-lifR
   - Status: drafted locally.
   - Package: `asset-folder/content/out-of-the-loop-on-claude-heres-10-must-have-marketing-skills`
   - Caption signal: Sonnet 5 is cheap but useful for marketing; it reads live ad data and returns a ranked fix list.
   - Image signal: accepted terminal-style graphic listing 10 Skills for performance marketers, split into 5 Meta Ads and 5 Google Ads commands.
   - CTA: caption uses `SONNET`; image footer uses `AUDIT`. Package follows caption CTA.

4. https://www.linkedin.com/posts/charlie-hills_claude-code-actually-runs-all-4-of-my-channels-activity-7484909992677036033-9G9i
   - Status: captured.
   - Feedshare images: 5.
   - Next action: analyze caption and accept only images matching the 4-channel Claude Code system.

5. https://www.linkedin.com/posts/charlie-hills_i-actually-replaced-myself-with-11-ais-activity-7484547615334805505-Yu-g
   - Status: drafted locally.
   - Package: `asset-folder/content/i-actually-replaced-myself-with-11-ais`
   - Feedshare images: 1.
   - Caption signal: 11 AI roles replaced one creator bottleneck while the human keeps the final approval.
   - Image signal: accepted org-chart visual titled `Your New AI Content Team`, with Charlie as CEO and 11 tool/AI department heads.
   - CTA: `TEAM`.

6. https://www.linkedin.com/posts/charlie-hills_claude-will-gaslight-you-until-you-install-activity-7484185211099078656-lA_W
   - Status: captured.
   - Feedshare images: 1.
   - Next action: analyze LLM Council visual plus caption before drafting.

7. https://www.linkedin.com/posts/ruben-hassid_if-you-already-knew-all-26-hacks-unfollow-activity-7487461879179726850-YQQ_
   - Status: captured.
   - Feedshare images: 3.
   - Next action: analyze hack-list visuals plus caption before drafting.

8. https://www.linkedin.com/posts/ruben-hassid_writing-emails-from-scratch-in-2026-is-embarrassing-activity-7487371217813934080-Vrpp
   - Status: captured.
   - Feedshare images: 8.
   - Next action: analyze exact activity caption/images separately from the earlier email workflow share.

9. https://www.linkedin.com/posts/ruben-hassid_delete-every-prompt-template-you-ever-saved-activity-7486737016571731968-9DoM
   - Status: captured.
   - Feedshare images: 7.
   - Next action: analyze caption/images and reject unrelated thumbnails before drafting.

10. https://www.linkedin.com/posts/ruben-hassid_dont-post-obvious-ai-written-content-activity-7486374672033316864-tYgN
    - Status: captured.
    - Feedshare images: 2.
    - Next action: analyze pyramid/AI-writing visuals plus caption before drafting.

11. https://www.linkedin.com/posts/ruben-hassid_you-could-spend-a-weekend-building-this-yourself-activity-7486646420314230785-ZZX0
    - Status: captured.
    - Feedshare images: 1.
    - Next action: analyze Drive-folder visual plus caption before drafting.

12. https://www.linkedin.com/posts/hasan-choudhry_are-you-using-claude-for-marketing-heres-activity-7485639931134971904-F1fo
    - Status: captured.
    - Feedshare images: 9.
    - Next action: analyze image set carefully and reject unrelated images before drafting.

13. https://www.linkedin.com/posts/hasan-choudhry_did-you-know-5-claude-agents-can-run-your-activity-7484913899276808192-cteA
    - Status: captured.
    - Feedshare images: 1.
    - Next action: analyze paid-media agents graphic plus caption before drafting.

14. https://www.linkedin.com/posts/hasan-choudhry_if-youre-out-of-the-loop-on-claude-heres-activity-7483827970009341953-Evat
    - Status: captured.
    - Feedshare images: 7.
    - Next action: analyze performance-marketer audit visuals plus caption before drafting.

15. https://www.linkedin.com/posts/hasan-choudhry_if-youre-a-creative-strategist-using-claude-activity-7483464272493322240-mgiK
    - Status: captured.
    - Feedshare images: 6.
    - Next action: analyze creative-strategist visuals plus caption before drafting.
