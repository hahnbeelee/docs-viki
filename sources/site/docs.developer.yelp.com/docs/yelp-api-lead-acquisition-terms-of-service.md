# Source: https://docs.developer.yelp.com/docs/yelp-api-lead-acquisition-terms-of-service

Terms of Service Version 1.02 
Effective Date: May 15, 2026

These Yelp Lead Acquisition API Terms of Service (these "Terms") govern the use of the Yelp Lead Acquisition API (the "API") by any party ("Partner" or "you") who executes an Insertion Order with Yelp Inc. ("Yelp") that references these Terms. By executing an Insertion Order, Partner agrees to be bound by these Terms.

 

1. **Purpose, Roles, and User Process (Introduction)** 
 1.1 This Agreement governs the relationship under which Yelp shall purchase consumer leads ("Leads") from the Partner using a dynamic bidding model. The Partner operates websites where a Homeowner (the consumer submitting the quote request) initiates a quote request by submitting their project type and location (e.g., zip code). The Partner then uses a Ping-Post API process, built and maintained by Yelp, to offer this potential Lead to Yelp for a bid. If Yelp submits the winning bid, the consumer completes the project submission on the Partner's site, and the Partner immediately transmits the consumer's PI (Personally Identifiable Information) and project details (the Lead) to Yelp via API. Yelp then assumes ownership of the Lead, utilizes the PI to create an account if necessary, and services the quote request by dispatching it to local Yelp Pros the local service professionals and businesses on the Yelp platform) who can respond to the consumer via email, app, or messaging inbox. Yelp acts solely as the Lead Buyer, with no volume commitments to the Partner, and the Partner warrants that all Leads sold to Yelp are exclusive to Yelp (i.e. are not sold to Yelp and other Lead buyers concurrently) and sourced only from its owned and operated websites. 
 1.2 **No Commitment**: : This Agreement does not create any commitment or obligation on the part of Yelp to purchase any minimum volume of Leads or continue the pilot for any fixed duration. Yelp reserves the right, in its sole discretion, to bid on, or to terminate the pilot at any time. 
 1.3 **Commercial Schedules and Order of Precedence:** The specific commercial terms, including the agreed-upon rates, criteria for Leads, and delivery dates, shall be set forth in a separate Insertion Order (IO) or Order Form in the form of the attached Exhibit B (each, a "Schedule"), which shall be deemed incorporated into this Agreement upon execution by both Parties. In the event of an irreconcilable conflict between the terms of any executed Schedule and this Agreement, the terms of this Agreement shall control, except for the financial rate and volume criteria expressly set forth in the Schedule.
2. **Lead Requirements and Sourcing** 
 The parties agree to the following mandatory conditions for all Leads offered to and purchased by Yelp: 
 2.1 **Lead Exclusivity**: All Leads purchased by Yelp must be exclusive leads. Partner warrants that any Lead sold to Yelp has not been and will not be sold to any other buyer. 
 2.2 **Lead Sourcing**: All Leads offered to Yelp must be generated on Partner's owned and operated sites only (e.g., mygutterguards.com). Partner warrants that Leads are sourced exclusively via owned methods, excluding all 3rd party aggregators and affiliates unless explicitly agreed to by Yelp in writing, email sufficing. 
 2.3 **Lead Validation and Returns**: Yelp may, in its sole discretion, return any Lead purchased that contains obviously false information or disconnected contact information (e.g., telephone number, email address) within five (5) business days of receipt for credit against future invoices. Partner agrees to issue such credit promptly upon validation of the invalidity of the Lead. 
 2.4 **Transparency and Brand Disclosure**. To ensure the consumer’s original intent to be contacted by Yelp is preserved, Partner shall ensure that its consent UI clearly and conspicuously discloses Yelp’s role in fulfilling the quote request. This disclosure must be presented at the point of collection, in a font size and color that is easily readable and not overshadowed by other design elements. Specifically, the call-to-action (e.g., the "Submit" button) or the immediate surrounding text must explicitly state that the consumer is directing Partner to share their information with Yelp for the purpose of receiving quotes from Yelp service professionals. Upon the consumer clicking the call-to-action, Partner must immediately redirect the consumer (or, at a minimum, open a new browser window or tab) to a Yelp-specified landing page or confirmation URL. Failure to implement this redirection shall be considered a material breach of the Transparency requirements. Any material change to this disclosure or the surrounding UI/UX must be approved by Yelp in writing prior to implementation. 
 2.5 **Data Ping**. Partner agrees that during the initial API request used to solicit a bid from Yelp, Partner shall only transmit generalized project data, such as zip code and job category. Partner agrees that it will not include any Personally Identifiable Information (“PI”) in this pre-bid transmission, expressly including IP addresses, device identifiers, and any other consumer-specific data. Partner may only transmit Personally Identifiable Information after the consumer has affirmatively clicked the final submission button.
3. **Data Transfer and Privacy** 
 3.1 **Lead Transfer**: When a consumer completes a project submission on a Partner site and Yelp has the winning bid, the consumer's PI and project information will be passed to Yelp via API. 
 3.2 **Partner Data Warranty and Evidence of Consent**. PI Partner represents and warrants that all PI contained in the Leads has been collected and transferred to Yelp in full compliance with all applicable privacy laws, expressly including the CCPA, CPRA and the California Information Privacy Act (CIPA). Partner further represents and warrants that for every Lead provided, Partner has obtained legally valid Prior Express Consent and Prior Express Written Consent under the TCPA and analogous state laws. This consent must specifically identify Yelp by name at the point of collection and authorize Yelp and its service professionals to contact the consumer via automated technology, including auto-dialers, SMS, and artificial or prerecorded voice messages. To ensure the integrity of this consent, Partner shall retain a comprehensive "click-log" or similar digital record for each Lead for no less than five (5) years. This record must include the date and time of consent, the consumer’s IP address, and a visual representation (e.g., a screenshot or "session replay" link) of the exact UI/UX and disclosure text the consumer viewed. Upon Yelp’s written request, Partner shall provide this evidence of consent within three (3) business days to assist in the resolution of any consumer inquiry or regulatory matter. Partner also represents and warrants that, at the time of delivery to Yelp, no Lead contains a telephone number that is: (i) listed on the National Do Not Call Registry or any analogous state registry; or (ii) a reassigned number. Partner shall utilize a commercially reasonable scrubbing service (e.g., the FCC Reassigned Numbers Database) to verify compliance with this subsection (c) prior to each Lead transfer. 
 3.3 **Yelp Ownership and Service**: Upon receipt of the PI, Yelp will own and service the Lead and send the quote request to Yelp professionals (pros). Yelp’s use of the PI shall be governed by Yelp’s internal policies. 
 3.4 **Data Protection**: The Parties agree to comply with the terms of the Data Protection Addendum, attached hereto as Exhibit A, which governs the processing of Yelp Personal Information under this Agreement.

 

4. **Commercial Terms and Payment** 
 4.1 **Fee Model: Fee Model**: Yelp will pay Partner per Lead. 
 4.2 **Invoicing**: Partner shall invoice Yelp monthly for all Leads successfully sold to Yelp. Undisputed invoices are due and payable Net 45 days from the date of such invoice. 
 4.3 **Reporting**: Partner shall provide Yelp with bi-weekly status updates regarding: (i) lead volume trends; (ii) any technical issues with API integration; (iii) quality metrics; and (iv) any changes to Partner's lead generation practices or sources. In addition, Partner shall provide reporting to Yelp within two (2) business days of calendar month end that includes summary level metrics (total Leads, total spend) and itemized Leads transactions that include time/date stamp, lead price, originating site, and any other information reasonably requested by Yelp, email sufficing. 
 4.4 **Operational Updates**: Partner shall provide Yelp with regular status updates regarding the API integration, lead volume trends, quality metrics, and any material issues or changes affecting the delivery of Leads to Yelp, at a mutually agreed-upon frequency (e.g., bi-weekly or monthly).
5. **Term and Termination** 
 5.1 **Term**: This Agreement is effective as of the Effective Date and shall continue until terminated by either Party in accordance with this Section. 
 5.2 **Termination for Convenience**: Either Party may terminate this Agreement for convenience at any time by providing no less than thirty (30) days’ prior written notice to the other Party. This notice period aligns with the no-commitment nature of the pilot. 
 5.3 **Termination for Cause**: 
 (a) **Immediate Termination for Privacy/Consent Breach.** Notwithstanding any standard notice period or 
 the cure rights set forth below, Yelp may terminate this Agreement immediately upon written notice if 
 Partner breaches any privacy, data protection, or consumer consent warranty, including but not limited 
 to those set forth in Section 3.2 or Exhibit A. Yelp also reserves the right to unilaterally suspend API bidding 
 immediately if a consent violation or deceptive collection practice is suspected, without terminating the 
 entire Agreement. 
 (b) **Termination for Material Breach**. Either Party may terminate this Agreement if the other Party 
 materially breaches any of its obligations hereunder (other than the privacy and consent warranties 
 governed by subsection (a) above) and fails to cure such breach within thirty (30) days after receipt of 
 written notice describing the breach in reasonable detail. 
 5.4 **Effect of Termination**: Upon termination, Partner shall cease all use of the Yelp API and Yelp shall pay 
 for all Leads successfully received prior to the effective date of termination. 
 5.5 **Transition Assistance**: 
 (a) Termination. Upon termination, Partner shall: (i) immediately cease all use of the Yelp API and any 
 Yelp-provided credentials or access methods; (ii) within ten (10) business days, destroy all Yelp 
 Confidential Information in its possession, including but not limited to bid patterns, conversion metrics, 
 performance data, and any technical documentation related to the API integration; (iii) upon request, 
 provide written certification of such destruction within fifteen (15) business days of termination; and (iv) 
 cooperate reasonably with any technical disconnect requirements to ensure clean API disconnection. 
 (b) AI and Data Integrity. Partner agrees that it shall not, at any time during or after the term of this 
 Agreement: (i) share, disclose, or use Yelp's bid rates, conversion data, lead performance metrics, or any 
 other confidential performance data with any third party; (ii) use such information to benefit any other 
 lead buyer; (iii) fail to maintain appropriate data segregation if Partner works with Yelp competitors; or 
 (iv) use Yelp Content—including Customer Data, bid patterns, or any aggregate insights derived from 
 Yelp’s platform—to train, fine-tune, or improve any artificial intelligence or machine learning models. This 
 prohibition includes both generative models (e.g., LLMs) and non-generative models used for predictive 
 analytics. For clarity, "derivative works" in this context does not include individual business records created for a single transaction, but does include any aggregate insights or patterns harvested from Yelp’s 
 bid data or lead-acquisition activity. This obligation shall survive termination for three (3) years.
6. **No Non-Circumvention**: The Parties agree that neither Party shall be restricted from contracting with 
 any other publishers, lead sources, or lead buyers. Each Party is free to engage with any third parties for 
 similar services.
7. **Indemnity, Liability and Insurance** 
 7.1 **Partner Indemnity**: Partner will indemnify and defend Yelp from any claim arising out of or related to: 
 (a) Partner's breach of the Lead Exclusivity or Sourcing requirements (Section 2); (b) Partner's breach of 
 the privacy, data security, or consumer consent warranties set forth in Section 3.2, including any 
 allegations that Lead Data was collected in violation of the CCPA/CPRA or that Yelp lacked valid TCPA 
 consent; or (c) the operation of Partner's websites. 
 7.2 **Mutual Indemnity for General Breach**: Each Party (the “Indemnifying Party”) shall indemnify, defend 
 and hold harmless the other Party (the “Indemnified Party”) from and against any and all claims, suits, 
 losses, damages, liabilities, costs and expenses (including reasonable attorneys’ fees and expenses) arising 
 out of or relating to any material breach by the Indemnifying Party of its representations, warranties, 
 covenants, or obligations set forth in this Agreement, including but not limited to any breach of its data 
 protection, privacy, or confidentiality obligations. The Indemnified Party shall promptly notify the 
 Indemnifying Party of any such claim and provide reasonable cooperation for the defense thereof. 
 7.3 **Limitation of Liability**: 
 (a) Exclusion of Indirect Damages. NEITHER PARTY SHALL BE LIABLE FOR ANY SPECIAL, INCIDENTAL, 
 INDIRECT, EXEMPLARY, PUNITIVE, OR CONSEQUENTIAL DAMAGES OF ANY KIND WHATSOEVER. 
 (b) General Liability Cap. Except as expressly set forth in subsections (c) and (d) below, the maximum 
 aggregate liability of either Party for all claims shall in no event exceed the greater of (i) the total Fees 
 paid by Yelp to Partner in the twelve (12) months prior to the date the claim arose, or (ii) One Hundred 
 Thousand Dollars ($100,000.00). 
 (c) Enhanced Privacy and Consent Cap. Notwithstanding the General Liability Cap in subsection (b), 
 Partner's total aggregate liability for claims arising out of a breach of its TCPA or CCPA/CPRA warranties 
 in Section 3.2, or its corresponding indemnification obligations in Section 7.1, shall be capped at Five 
 Million Dollars ($5,000,000.00). 
 (d) Uncapped Liability. The limitations and caps set forth in subsections (b) and (c) above shall not apply 
 to a Party's liability for direct damages resulting from a breach of its Confidentiality obligations (Section 
 8.2), a breach of its Data Protection obligations (Exhibit A), or from willful misconduct or gross negligence, 
 all of which shall remain uncapped. 
 7.4 **Insurance**: Partner shall, at its sole expense, maintain insurance coverage sufficient to support its 
 indemnification obligations under this Agreement and to adequately cover risks associated with its 
 performance hereunder, including, without limitation: 
 (a) Commercial General Liability insurance with limits of at least $1,000,000 per occurrence and 
 $2,000,000 in the aggregate. 
 (b) Professional Liability (Errors & Omissions) insurance, including coverage for intellectual property 
 infringement claims, with limits of at least $1,000,000 per occurrence and $2,000,000 in the aggregate. 
 (c) Cyber Liability insurance covering breaches of confidentiality and privacy law violations, with limits of 
 at least $1,000,000 per occurrence and $5,000,000 in the aggregate. 
 Partner shall provide Yelp with certificates of insurance upon request, naming Yelp as an additional 
 insured with respect to coverage for IP infringement, confidentiality breaches, and privacy law claims 
 arising from Partner's performance under this Agreement. This insurance obligation shall remain in effect 
 during the Term of this Agreement and for a period of three (3) years following its termination or 
 expiration.
8. **General Provisions** 
 8.1 **Dispute Resolution**: 
 (a) Arbitration. Any controversy or claim arising out of or relating to this Agreement, or the breach thereof, 
 shall be settled by final and binding arbitration administered by National Arbitration and Mediation 
 ("NAM"), or if NAM is unavailable, by another mutually agreed arbitral forum, and governed by NAM's 
 Comprehensive Dispute Resolution Rules and Procedures ("NAM Rules"), which are available at 
 [www.namadr.com.](http://www.namadr.com.) The arbitration shall be conducted by a single, neutral arbitrator. This arbitration 
 agreement evidences a transaction involving interstate commerce and, notwithstanding the provision 
 below with respect to the applicable substantive law, the Federal Arbitration Act, 9 U.S.C. §1 et seq. will 
 govern the interpretation and enforcement of this arbitration agreement. The arbitration hearing will take 
 place in San Francisco, California, unless otherwise mutually agreed to by the parties. 
 (b) Choice of Law. The arbitrator shall apply the substantive law of California, without regard to its conflict- 
 of-law principles. 
 (c) Arbitrator's Authority. The arbitrator shall have the exclusive authority to determine the scope and 
 enforceability of this Arbitration Agreement, including any claim that all or any part of this Arbitration 
 Agreement is void or voidable. The arbitrator will have the authority to award monetary damages, 
 injunctive relief, and any other remedies available under applicable law, consistent with the terms of this 
 Agreement. The arbitrator may order the imposition of sanctions which may include, but are not limited 
 to, assessment of arbitration fees and costs, attorneys’ fees, and/or any other costs resulting from the 
 sanctionable conduct. The arbitrator's decision will include a reasoned award detailing the essential 
 findings and conclusions on which the award is based. The award may be confirmed in any court of 
 competent jurisdiction. 
 (d) Fees and Costs. Subject to the arbitrator’s authority to impose sanctions, each Party shall bear its own 
 attorneys' fees and costs during the arbitration. After the arbitration is declared closed, the arbitrator may 
 award the total costs of the arbitration and/or the cost of legal representation to one Party or may 
 apportion such costs between the parties if the arbitrator determines that apportionment is appropriate. 
 (e) Jury Trial and Class Action Waiver. THE PARTIES EXPRESSLY WAIVE THE RIGHT TO TRIAL BY JURY. The 
 parties further acknowledge and agree that any arbitration will be conducted on an individual basis only. 
 There shall be no right or authority for any claims to be arbitrated or resolved on a class, collective, or 
 consolidated basis, or in a representative capacity. The arbitrator may not consolidate more than one 
 Party's claims and may not otherwise preside over any form of a representative or class proceeding. 
 (f) Injunctive Relief. Notwithstanding the parties’ agreement to arbitrate, each Party retains the right to 
 seek injunctive or other equitable relief in a court of competent jurisdiction to prevent the actual or 
 threatened infringement, misappropriation or violation of a Party’s copyrights, trademarks, trade secrets, 
 patents or other intellectual property rights. 
 8.2 **Confidentiality**: The terms and conditions of this Agreement will be the Confidential Information of 
 the Parties. Each Party agrees to: (a) use Confidential Information solely for the purposes of performing 
 its obligations under this Agreement; (b) not disclose Confidential Information to any third-party without 
 the prior written consent of the disclosing Party, except as required by law; (c) implement and maintain 
 reasonable security measures to prevent unauthorized access, use, or disclosure of Confidential 
 Information; and (d) ensure that its employees, contractors, and agents who have access to Confidential 
 Information are bound by confidentiality obligations at least as restrictive as those herein. 
 Partner acknowledges that Yelp's bid rates, conversion data, lead performance metrics, and operational 
 details specifically related to Yelp's use of Leads or pertaining to individual Yelp campaigns ("Yelp-Specific 
 Performance Data") constitute sensitive competitive information. Partner shall not share, disclose, or use 
 Yelp-Specific Performance Data, or any aggregate patterns, synthetic datasets, or derivative works created 
 from such data, to train, fine-tune, or improve any artificial intelligence or machine learning models. This 
 prohibition includes inputting Yelp-Specific Performance Data into any third-party service for such 
 purposes. To maintain the integrity of Yelp’s lead-buying logic, Yelp may, at its discretion, seed or 
 "watermark" bid data in a manner that does not materially impact the quality or performance of the API 
 for the purpose of verifying compliance with these restrictions. Partner shall implement and maintain 
 internal controls, such as data segregation and access restrictions, to ensure that Yelp-Specific 
 Performance Data is isolated from information pertaining to Partner's other clients. If Partner is required 
 by law to disclose Confidential Information, it shall notify the disclosing Party within five (5) business days 
 and cooperate to limit disclosure to the minimum required. 
 8.3 **Assignment**: Neither Party may assign this Agreement without the prior written consent of the other 
 Party; provided, however, that either Party may assign this Agreement to an affiliate or in connection with 
 a merger, acquisition, or sale of all or substantially all its assets without such consent, upon written notice 
 to the other Party. 
 8.4 **Audit Rights.** Yelp retains the right to audit Partner's live landing pages and consent flows at any time 
 during the term of this Agreement to verify ongoing compliance with all transparency and consent 
 requirements. Upon written request, Partner shall provide Yelp with sample click-logs or digital consent 
 records within three business days. If Yelp identifies any user interface changes or testing variations that 
 obscure the required legal disclosures, Partner shall immediately revert to the approved design. 
 8.5 **Entire Agreement**: This Agreement, including Exhibit A, constitutes the entire agreement between the Parties regarding the subject matter herein. 
 8.6 **Survival**: The termination or expiration of this Agreement shall not affect the rights and obligations of the Parties that are intended to survive such termination or expiration. Accordingly, the following core provisions shall survive the termination or expiration of this Agreement for any reason: all obligations related to Lead Requirements and Sourcing (Section 2), Data Transfer and Privacy (Section 3), and the Data Protection Addendum (Exhibit A), including the Partner's data warranties, indemnities, and data deletion obligations. Furthermore, the financial settlement for all Leads successfully received prior to termination (Section 5.3), the obligations under Transition Assistance (Section 5.4), the explicit clause on No Non-Circumvention (Section 6), all terms governing Indemnity, Liability, and Insurance (Section 7), Dispute Resolution (Section 8.1), the protection of Confidentiality (Section 8.2) and this Section 8.5 shall remain in full force and effect.

**EXHIBIT A 
DATA PROTECTION ADDENDUM** 
This Data Protection Addendum ("**Addendum**") is entered into by and between any party ("**Partner**" or 
"**you**") who executes an Insertion Order with Yelp Inc. ("**Yelp**") that references this Addendum and Yelp 
Inc. ("**Yelp**" in this Addendum) to cover the exchange of Personal Information shared by Partner with Yelp 
to perform the Business Purpose as set forth in the Agreement ("**Business Purpose**"). 
Partner and Yelp may each be referred to as a "Party" and/or collectively referred to as the "Parties".

1. **Definitions**. 
 A. **"Aggregated" or "Deidentified"** shall have the meanings as ascribed by Privacy Laws and all regulations 
 and opinions issued related thereto. 
 B. "**Yelp Personal Information"** means any information that identifies, relates to, describes, is capable of 
 being associated with, or could reasonably be linked, directly or indirectly, with a particular individual or 
 household, that may be: (i) processed at any time by Partner in anticipation of, in connection with or 
 incidental to the performance of this Addendum, including any information provided by or on behalf of 
 Partner to Yelp, or (ii) derived by Partner from such information. Personal Information includes any data 
 elements identified pursuant to Privacy Laws. 
 C. **"Consumer," "Processing" (or "process"), "Share," and "Sale,"** (including the terms "sell," "selling," 
 "sold," and other variations thereof) shall have the meanings ascribed to those terms under the Privacy 
 Laws. 
 D. **"Privacy Laws"** may include, without limitation, as applicable under the circumstances pertaining to 
 the collection or sharing of data, Cal. Civ. Code §§ 1798.100 et seq., as amended by the California Privacy 
 Rights Act of 2020 (the California Consumer Privacy Act) ("CCPA"), Colo. Rev. Stat. §§ 6-1-1301 et seq. (the 
 Colorado Privacy Act) ("CPA"), Connecticut's Data Privacy Act ("CTDPA"), Utah Code Ann. §§ 13-61-101 et 
 seq. (the Utah Consumer Privacy Act) ("UCPA"), VA Code Ann. §§ 59.1-575 et seq. (the Virginia Consumer 
 Data Protection Act) ("VCDPA") (collectively "Privacy Laws"), and the European Union General Data 
 Protection Regulation (Regulation (EU) 2016/679) ("GDPR"), and applicable subordinate legislation and 
 regulations implementing those laws. This Addendum acknowledges that Privacy Laws and regulations 
 are subject to change and that new privacy laws may be enacted or take effect during the term of this 
 Addendum. Partner agrees that any additional privacy laws that come into effect during the term of this 
 Addendum shall automatically apply to the processing of Yelp Personal Information covered by this 
 Addendum, without the need for further amendments. Any conflicts between the existing provisions of 
 this Addendum and the new privacy laws shall be resolved in favor of the new privacy laws to the extent 
 permitted by applicable legal requirements and solely to the extent necessary to comply with Privacy 
 Laws.
 
2. **Privacy Law Compliance. 
 **A. Partner acknowledges and agrees that it shall process Yelp Personal Information solely as necessary to 
 perform its obligations under this Addendum for the Business Purpose described herein (i.e., offering 
 Leads to Yelp via a Ping-Post dynamic bidding process, and where Yelp has the winning bid, transferring 
 consumer PI and project information to Yelp). Partner shall not: (a) sell or share Yelp Personal Information; 
 or (b) retain, use or disclose Yelp Personal Information for any purpose other than for the Business 
 Purpose. Partner hereby certifies that it understands the foregoing restrictions and that it shall comply 
 with such restrictions. In no event shall Partner process the Yelp Personal Information for its own purposes 
 or those of any third-party; provided however, Partner may utilize Yelp Personal Information in the 
 Aggregated and Deidentified manner in connection with Partner's ordinary business practices, provided 
 that: 
 (i) it has implemented technical safeguards that prohibit reidentification of such deidentified 
 information, including but not limited to removing all direct and indirect identifiers as required by 
 Privacy Laws; 
 (ii) it has implemented business processes that specifically prohibit the reidentification and 
 inadvertent release of such information; 
 (iii) Partner represents and warrants that all such aggregation and deidentification will be 
 performed in compliance with all applicable Privacy Laws and industry best practices, including 
 CCPA standards for deidentification; and 
 (iv) Partner shall indemnify, defend, and hold harmless Yelp from any claims, losses, or damages 
 arising from Partner's failure to properly aggregate or deidentify such information, with such 
 indemnification obligation being unlimited and not subject to any liability cap in the Agreement. 
 B. Partner hereby certifies, represents, warrants and covenants that it understands its obligations under 
 the Privacy Laws and that it shall comply at all times with the Privacy Laws and this Addendum, and shall 
 provide Yelp with all reasonably requested assistance and cooperation to enable Yelp to comply with and 
 fulfill its obligations under Privacy Laws. Without limiting the foregoing, Partner shall, upon Yelp's request, 
 cooperate in good faith with Yelp to modify the terms herein and/or enter into additional terms to address 
 any modifications, amendments or updates to the Privacy Laws and/or other industry guidelines. 
 C. Partner is prohibited from combining or otherwise associating Yelp Personal Information with any other 
 data associated with the same underlying consumer, device, identifier, except as necessary to perform its 
 obligations under the Agreement. Where it is necessary to perform its obligations under this Addendum 
 by combining or otherwise associating Yelp Personal Information with other data associated with the 
 same underlying consumer, device, or identifier, Partner will disassociate such Yelp Personal Information 
 from such other data once it has completed its obligation under the Agreement with respect to such Yelp 
 Personal Information. 
 D. Partner represents, warrants, and covenants that: 
 ((i) All Personal Information will be collected, processed, and transferred in full compliance with applicable 
 Privacy Laws; 
 (ii) Any aggregation or deidentification of Personal Information will be performed using methods that 
 prevent reidentification by Partner or any third party; 
 (iii) Partner has implemented and will maintain technical and organizational measures sufficient to protect 
 Personal Information against accidental or unlawful destruction, loss, alteration, or unauthorized 
 disclosure; 
 (iv) Except for claims arising from a breach of the consent collection and transfer warranties set forth in 
 Section 3.2 of the Agreement, which shall be subject to the specific liability cap in Section 7.3(c), Partner's 
 breach of any obligation related to Personal Information protection, aggregation, deidentification, or 
 Privacy Law compliance post-transfer shall not be subject to any limitation of liability, and Partner accepts 
 unlimited liability for any such breaches.
 
3. **Inquiries**. In the event that Partner receives an Inquiry (as defined below), Partner shall: (a) notify Yelp 
 in writing of the Inquiry within two (2) business days (or such other time period as Yelp may specify in 
 writing from time to time); (b) comply with all instructions from Yelp regarding the response to such 
 Inquiry; (c) if requested, promptly and in any case, within seventy-two (72) hours) provide Yelp with copies 
 of documents relating to the Inquiry; (d) not refer to Yelp in any correspondence or other response to the 
 Inquiry without Yelp's prior written consent; (e) not disclose any confidential information of Yelp to the 
 applicable individual, third-party or authority without Yelp's prior written consent; and (f) in a timely 
 manner, notify Yelp of, and permit a representative of Yelp to attend, any relevant inspections or 
 proceedings. Partner shall take all other measures as requested by Yelp to respond to or otherwise 
 address the Inquiry adequately and in a timely manner. As used herein, "Inquiry" means any request, 
 correspondence, inquiry or complaint (including rights of access or deletion, as applicable) received from 
 Yelp, or other individual or regulatory authority in connection with the processing of Yelp Personal 
 Information. Partner may notify Yelp at [dataprotection@yelp.com](mailto:dataprotection@yelp.com).
 
4. **Security Measures**. Partner shall implement and maintain technical and organizational security 
 measures appropriate under applicable Privacy Laws to protect the Yelp Personal Information from: (1) 
 accidental, unauthorized or unlawful destruction, loss, alteration, disclosure or access; and (2) 
 unauthorized or unlawful processing (each, a "Security Incident"). The technical and organizational 
 measures implemented by Partner must ensure a level of security commensurate with the risks presented 
 by the nature and processing of such Yelp Personal Information. Such measures shall, at minimum, meet 
 or exceed industry standards and best practices (e.g., SOC 2 compliance). Such measures shall specifically 
 include, without limitation: 
 (a) Encryption of all Personal Information in transit using Transport Layer Security (TLS) version 
 1.2 or higher, with strong cipher suites excluding any known vulnerable protocols; 
 (b) Encryption of Personal Information at rest using AES-256 encryption or equivalent industry- 
 standard encryption; 
 (c) Secure key management practices in accordance with NIST guidelines; 
 (d) Implementation of perfect forward secrecy for all API communications; 
 (e) Regular security assessments and penetration testing at least annually; and 
 (f) Maintenance of SOC 2 Type II certification or equivalent third-party security audit certification. 
 Partner shall also ensure that all Partner personnel receive appropriate training regarding the 
 requirements herein with respect to Privacy Law compliance, privacy and data security, and, if requested 
 by Yelp, shall promptly certify in writing that such training has taken place.
 
5. **Security Incidents**. In addition to any obligations set forth in the Agreement and applicable law, upon 
 becoming aware of any actual or reasonably suspected Security Incident which adversely impacts Yelp 
 Personal Information, Partner shall inform Yelp without undue delay, and in any event within forty-eight 
 (48) hours following discovery thereof. Partner shall cooperate with Yelp, including without limitation, by 
 providing Yelp with all information necessary, or otherwise requested by Yelp, in order to investigate such 
 Security Incident (including without limitation, the names of all individuals who are affected by the 
 Security Incident and the date, time and cause of such Security Incident). Partner shall, at its sole expense, 
 take all measures and actions necessary to remedy or mitigate the effects of the Security Incident and 
 shall keep Yelp informed of all developments in connection with such investigation, remediation and 
 mitigation. Notwithstanding the foregoing, Partner shall not issue any notification or other 
 communications to the impacted individuals or applicable regulatory bodies without Yelp's prior written 
 consent. Partner shall pay, or reimburse Yelp, for all costs, expenses, fines and other amounts incurred in 
 connection with the response to and remediation of the Security Incident by Partner and Yelp. 
 Partner acknowledges and agrees that its obligations under this Section 5, including but not limited to 
 reimbursement of all costs, expenses, and fines, are not subject to any limitation of liability provisions in 
 the Agreement. Partner further agrees that any failure to properly aggregate, deidentify, encrypt, or 
 otherwise protect Personal Information as required herein shall be deemed a Security Incident subject to 
 this Section. For the avoidance of doubt, a failure to obtain valid CCPA, CPRA, or TCPA consents prior to 
 transferring Lead Data to Yelp shall not constitute a Security Incident under this Addendum.
 
6. **Deletion or Return of Data.** Upon termination or expiration of the Agreement, Partner shall destroy 
 (or, at Yelp's election, return to Yelp or its designee) all Yelp Personal Information (including all copies and 
 backups of the Yelp Personal Information, whether in written, electronic or other form or media) in its 
 possession or control. At Yelp's request, Partner shall provide Yelp within ten (10) business days of such 
 revocation, expiration or termination of such rights with a certificate in form and substance satisfactory 
 to Yelp that such Yelp Personal Information has been destroyed. If Partner is required by applicable law 
 to retain some or all of the Yelp Personal Information, Partner shall (and shall ensure that Partner 
 personnel) protect such Yelp Personal Information pursuant to the terms herein (and prevent any further 
 processing of such information) and shall destroy or return the Yelp Personal Information in accordance 
 with this provision as soon as retention of the Yelp Personal Information is no longer required.
 
7. **Audit and Security Questionnaire**. Upon Yelp's request (not more than annually, unless a Security 
 Incident occurs or Yelp reasonably suspects material non-compliance), Partner shall promptly complete 
 Yelp's written security and compliance questionnaire regarding its adherence to this Addendum. Beyond 
 technical security, Yelp (or its third-party auditor) shall have the right to audit Partner's lead-generation 
 flows, user interfaces, and disclosure placement to verify that the collection of Yelp Personal Information 
 is not "deceptive" or "unfair" under FTC standards or California’s Unfair Competition Law (UCL § 17200). 
 Partner shall provide copies of all consumer-facing screens, terms of service, and consent mechanisms 
 used to source Leads for Yelp. If such a review reveals material deficiencies in how consent is captured or 
 how Yelp’s brand is presented, Partner shall promptly remedy any identified deficiencies. If Partner fails 
 to cure a material non-compliance with Privacy Laws or these transparency standards within thirty (30) 
 days of notice, Yelp may terminate this Agreement.
 
8. **Partner Acknowledgement**. Partner certifies that it understands its restrictions and obligations set 
 forth above and will comply with them.
 

Updated about 1 month ago

---

Did this page help you?

Yes

No

Copy Page