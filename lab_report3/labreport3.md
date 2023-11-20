# Lab Report 3  Bugs and Commands (Week 5)

## Part 1

### Here is JUnit test code for failure-inducing input for the buggy program, the averageWithoutLowest; - (1)

```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {

  @Test
  public void testAverageWithoutLowest_Failure(){
    double[] input = {1.0, 1.0, 3.0, 4.0};
    double result = ArrayExamples.averageWithoutLowest(input);
    assertEquals(3.5, result, 0.0001);
  }
}
```

### Here's the JUnit test code for the non-failure-inducing input for the buggy program, the averageWithoutLowest; - (2)
```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
@Test
  public void testAverageWithoutLowerst_Success(){
    double[] input = {2.0, 3.0, 4.0};
    double result = ArrayExamples.averageWithoutLowest(input);
    assertEquals(3.5, result, 0.0001);
}
```

### The symptom
(1);
![Image](failure.png)

(2);
![Image](non-failure.png)

### The bug

Here is the buggy averageWithoutLowest method:

```
public class ArrayExamples {

  static double averageWithoutLowest(double[] arr) {
      if(arr.length < 2) { return 0.0; }
      double lowest = arr[0];
      for(double num: arr) {
        if(num < lowest) { lowest = num; }
      }
      double sum = 0;
      for(double num: arr) {
        if(num != lowest) { sum += num; }
      }
      return sum / (arr.length - 1);
    }

}
```

Here is the fixed averageWithoutLowest method:
```
static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    int lowestCount = 0;
    for(double num: arr) {
      if(num < lowest) {
        lowest = num;
        lowestCount = 1;
      } else if (num == lowest) {
        lowestCount++;
      }
    }
    double sum = 0;
    for(double num: arr) {
      sum += num;
    }
    return (sum - lowest * lowestCount) / (arr.length - lowestCount);
  }

```
output;
![Image](output.png)

### Why the Fix Addresses the Issue

It checks if the array has fewer than two elements. If so, it returns 0.0 because I can't compute an average without at least two numbers (excluding the lowest).
It initializes lowest with the first element and sets lowestCount to 0.
It iterates through the array to find the lowest number and counts how many times this lowest number appears.
It sums up all the numbers in the array.
It calculates the average by subtracting the total value of the lowest number(s) from the sum and dividing by the number of elements minus the count of the lowest number(s).
This logic ensures that if there are multiple instances of the lowest number, all are excluded from the average calculation.
    
## part 2

### 1. Using the -name option
The -name option allows you to search for files or directories that match a given pattern.
#### Citation of resource for this option
“Find Command in Linux with Practical Examples.” TecAdmin, 23 Mar. 2023, https://tecadmin.net/linux-find-command-with-examples/. 
Example 1: Finding a file by name
```
$ find ./technical -type f  -name "chapter*.txt"
```
Output:
![Image](option_name_file.png)
This command searches for files (-type f) named chapter*.name within the ./technical directory and its subdirectories. * is used to create a pattern. It's useful for locating all instances of files with a specific name.

Markdown for the Output:
```
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-1.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-7.txt
./technical/911report/chapter-9.txt
./technical/911report/chapter-8.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-10.txt
./technical/911report/chapter-11.txt
```
Example 2: Finding a directory by name
```
$ find ./technical -type d  -name "A*"  
```
Output:
![Image](option_name_directory.png)
This command searches for directories (-type d) named A* within the ./technical directory. * is used to create a pattern. This is useful for locating directories with a specific name.

Markdown for the Output:
```
./technical/government/About_LSC
./technical/government/Alcohol_Problems
```
### 2. Using the -iname option

The -iname option is similar to -name, but it is case-insensitive, making it useful for when the exact case of the target files or directories is unknown or mixed.

Example 1: Case-insensitive file search
```
$ find ./technical -type f -iname "*E*"
```
Output:
![Image](option_iname_file.png)
This command searches for any file with a case-insensitive match to * E *. It's useful when you are unsure of the case used in the file names.

Markdown for the Output:
```
./technical/government/About_LSC/LegalServCorp_v_VelazquezSyllabus.txt
./technical/government/About_LSC/Progress_report.txt
./technical/government/About_LSC/Strategic_report.txt
./technical/government/About_LSC/Comments_on_semiannual.txt
./technical/government/About_LSC/Special_report_to_congress.txt
./technical/government/About_LSC/commission_report.txt
./technical/government/About_LSC/LegalServCorp_v_VelazquezDissent.txt
./technical/government/About_LSC/ONTARIO_LEGAL_AID_SERIES.txt
./technical/government/About_LSC/LegalServCorp_v_VelazquezOpinion.txt
./technical/government/About_LSC/diversity_priorities.txt
./technical/government/About_LSC/reporting_system.txt
./technical/government/About_LSC/State_Planning_Report.txt
./technical/government/About_LSC/Protocol_Regarding_Access.txt
./technical/government/About_LSC/ODonnell_et_al_v_LSCdecision.txt
./technical/government/About_LSC/conference_highlights.txt
./technical/government/About_LSC/State_Planning_Special_Report.txt
./technical/government/Env_Prot_Agen/section-by-section_summary.txt
./technical/government/Env_Prot_Agen/jeffordslieberm.txt
./technical/government/Env_Prot_Agen/ro_clear_skies_book.txt
./technical/government/Env_Prot_Agen/1-3_meth_901.txt
./technical/government/Env_Prot_Agen/tech_sectiong.txt
./technical/government/Env_Prot_Agen/tech_adden.txt
./technical/government/Alcohol_Problems/Session2-PDF.txt
./technical/government/Alcohol_Problems/Session3-PDF.txt
./technical/government/Alcohol_Problems/DraftRecom-PDF.txt
./technical/government/Alcohol_Problems/Session4-PDF.txt
./technical/government/Gen_Account_Office/Testimony_cg00010t.txt
./technical/government/Gen_Account_Office/GovernmentAuditingStandards_yb2002ed.txt
./technical/government/Gen_Account_Office/Sept27-2002_d02966.txt
./technical/government/Gen_Account_Office/Statements_Feb28-1997_volume.txt
./technical/government/Gen_Account_Office/pe1019.txt
./technical/government/Gen_Account_Office/Testimony_Jul15-2002_d02940t.txt
./technical/government/Gen_Account_Office/Letter_Walkeraug17let.txt
./technical/government/Gen_Account_Office/Testimony_d01609t.txt
./technical/government/Gen_Account_Office/Sept14-2002_d011070.txt
./technical/government/Gen_Account_Office/June30-2000_gg00135r.txt
./technical/government/Gen_Account_Office/InternalControl_ai00021p.txt
./technical/government/Gen_Account_Office/Testimony_Jul17-2002_d02957t.txt
./technical/government/Gen_Account_Office/Paper_Walker11-2002_acpro122.txt
./technical/government/Gen_Account_Office/Letter_WalkerJan30-2001.txt
./technical/government/Post_Rate_Comm/Gleiman_EMASpeech.txt
./technical/government/Post_Rate_Comm/Mitchell_spyros-first-class.txt
./technical/government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt
./technical/government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt
./technical/government/Post_Rate_Comm/Mitchell_RMVancouver.txt
./technical/government/Post_Rate_Comm/Gleiman_gca2000.txt
./technical/government/Post_Rate_Comm/Cohenetal_Cost_Function.txt
./technical/government/Post_Rate_Comm/Redacted_Study.txt
./technical/government/Post_Rate_Comm/Mitchell_6-17-Mit.txt
./technical/government/Post_Rate_Comm/Cohenetal_comparison.txt
./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt
./technical/government/Post_Rate_Comm/Cohenetal_RuralDelivery.txt
./technical/government/Post_Rate_Comm/ReportToCongress2002WEB.txt
./technical/government/Post_Rate_Comm/WolakSpeech_usps.txt
./technical/government/Media/Federal_agency.txt
./technical/government/Media/water_fees.txt
./technical/government/Media/Helping_Out.txt
./technical/government/Media/balance_scales_of_justice.txt
./technical/government/Media/BusinessWire2.txt
./technical/government/Media/Legal-aid_chief.txt
./technical/government/Media/Funding_cuts_force.txt
./technical/government/Media/Good_guys_reward.txt
./technical/government/Media/Anthem_Payout.txt
./technical/government/Media/Donald_Hilliker.txt
./technical/government/Media/Free_legal_service.txt
./technical/government/Media/Owning_a_Piece.txt
./technical/government/Media/Targeting_Domestic_Violence.txt
./technical/government/Media/highlight_Senior_Day.txt
./technical/government/Media/State_funding.txt
./technical/government/Media/Few_who_need.txt
./technical/government/Media/City_Council_Budget.txt
./technical/government/Media/Legal_system_fails_poor.txt
./technical/government/Media/Supporting_Legal_Center.txt
./technical/government/Media/Lindsays_legacy.txt
./technical/government/Media/New_funding_sources.txt
./technical/government/Media/Barnes_new_job.txt
./technical/government/Media/Providing_Legal_Aid.txt
./technical/government/Media/Legal_Aid_in_Clay_County.txt
./technical/government/Media/Domestic_Violence_Ruling.txt
./technical/government/Media/Abuse_penalties.txt
./technical/government/Media/Law_Award_from_College.txt
./technical/government/Media/Raising_the_Bar.txt
./technical/government/Media/Justice_for_all.txt
./technical/government/Media/agency_expands.txt
./technical/government/Media/Helping_Hands.txt
./technical/government/Media/Legal_hotline.txt
./technical/government/Media/not_accessible_to_disabled.txt
./technical/government/Media/New_Online_Resources.txt
./technical/government/Media/Annual_Fee.txt
./technical/government/Media/Oregon_Poor.txt
./technical/government/Media/Barnes_pro_bono.txt
./technical/government/Media/Poor_Lacking_Legal_Aid.txt
./technical/government/Media/Paralegal_Honored.txt
./technical/government/Media/Workers_aid_center.txt
./technical/government/Media/Philly_Lawyers.txt
./technical/government/Media/Too_Crucial_to_Take_Cut.txt
./technical/government/Media/Pro_Bono_Services.txt
./technical/government/Media/Rumble_in_the_Bronx.txt
./technical/government/Media/FortWorthStarTelegram.txt
./technical/government/Media/predatory_loans.txt
./technical/government/Media/Survey.txt
./technical/government/Media/AP_LawSchoolDebts.txt
./technical/government/Media/Working_for_Free.txt
./technical/government/Media/Eviction_law.txt
./technical/government/Media/FY_04_Budget_Outlook.txt
./technical/government/Media/help_rent-to-own_tenants.txt
./technical/government/Media/Texas_Lawyer.txt
./technical/government/Media/Disaster_center.txt
./technical/government/Media/Higher_Registration_Fees.txt
./technical/government/Media/Fire_Victims_Sue.txt
./technical/government/Media/Funds_Shortage.txt
./technical/government/Media/Terrorist_Attack.txt
./technical/government/Media/Butler_Co_attorneys.txt
./technical/government/Media/BergenCountyRecord.txt
./technical/government/Media/families_saved.txt
./technical/government/Media/Court_Keeps_Judge_From.txt
./technical/government/Media/Volunteers_Step_Up.txt
./technical/government/Media/Coup_Reshapes_Legal_Aid.txt
./technical/government/Media/IOLTA_INTEREST_RATE.txt
./technical/government/Media/Ginny_Kilgore.txt
./technical/government/Media/Legal_Aid_looks_to_legislators.txt
./technical/government/Media/Poverty_Lawyers.txt
./technical/government/Media/Wingates_winds.txt
./technical/government/Media/Avoids_Budget_Cut.txt
./technical/government/Media/grants_fail_to_come.txt
./technical/government/Media/Lockyer_Warns.txt
./technical/government/Media/Self-Help_Website.txt
./technical/government/Media/Rental_rules.txt
./technical/government/Media/Using_Tech_Tools.txt
./technical/government/Media/Assuring_Underprivileged.txt
./technical/government/Media/Boone_legal_service.txt
./technical/government/Media/Firm_to_the_Poor_Needs_Help.txt
./technical/government/Media/Making_a_case.txt
./technical/government/Media/Barnes_Volunteers.txt
./technical/government/Media/Commercial_Appeal.txt
./technical/government/Media/Justice_requests.txt
./technical/government/Media/Free_Legal_Assistance.txt
./technical/government/Media/Local_Attorneys.txt
./technical/government/Media/Texas_Supreme_Court.txt
./technical/government/Media/Civil_Matters.txt
./technical/government/Media/Low-income_children.txt
./technical/government/Media/man_on_national_team.txt
./technical/government/Media/BusinessWire.txt
./technical/government/Media/The_Columbian.txt
./technical/government/Media/Higher_court.txt
./technical/government/Media/Service_Agency.txt
./technical/government/Media/Marylands_Legal_Aid.txt
./technical/government/Media/Bias_on_the_Job.txt
./technical/government/Media/Attorney_gives_his_time.txt
./technical/government/Media/Library_Lawyers.txt
./technical/government/Media/Crains_New_York_Business.txt
./technical/government/Media/Hard_to_Get.txt
./technical/government/Media/The_State_of_Pro_Bono.txt
./technical/government/Media/residents_sue_city.txt
./technical/government/Media/Legal_Aid_Society.txt
./technical/government/Media/GreensburgDailyNews.txt
./technical/government/Media/Major_Changes.txt
./technical/government/Media/Program_Lodges.txt
./technical/government/Media/Wilmington_lawyer.txt
./technical/government/Media/All_May_Have_Justice.txt
./technical/government/Media/Domestic_violence_aid.txt
./technical/government/Media/Advocate_for_Poor.txt
./technical/government/Media/fight_domestic_abuse.txt
./technical/government/Media/CommercialAppealMemphis2.txt
./technical/government/Media/Weak_economy.txt
./technical/government/Media/Lawyer_Web_Survey.txt
./technical/government/Media/Valley_Needing_Legal_Services.txt
./technical/government/Media/Barr_sharpening_ax.txt
./technical/government/Media/Legal_Aid_attorney.txt
./technical/government/Media/The_Bend_Bulletin.txt
./technical/government/Media/Legal_services_for_poor.txt
./technical/government/Media/Farm_workers.txt
./technical/government/Media/Entities_Merge.txt
./technical/government/Media/less_legal_aid.txt
./technical/government/Media/Understanding.txt
./technical/government/Media/Do-it-yourself_divorce.txt
./technical/government/Media/Politician_Practices.txt
./technical/government/Media/defend_yourself.txt
./technical/government/Media/Towson_Attorney.txt
./technical/government/Media/A_Perk_of_Age.txt
./technical/government/Media/A_helping_hand.txt
./technical/government/Media/pro_bono_efforts.txt
./technical/government/Media/5_Legal_Groups.txt
./technical/government/Media/Greedy_Generous.txt
./technical/government/Media/Retirement_Has_Its_Appeal.txt
./technical/government/Media/RoanokeTimes.txt
./technical/government/Media/NJ_Legal_Services.txt
./technical/government/Media/Bridging_legal_aid_gap.txt
./technical/government/Media/Legal_Aid_campaign.txt
./technical/government/Media/Aid_Gets_7_Million.txt
./technical/.DS_Store
./technical/plos/pmed.0020273.txt
./technical/plos/pmed.0020065.txt
./technical/plos/pmed.0020071.txt
./technical/plos/pmed.0020059.txt
./technical/plos/pmed.0010039.txt
./technical/plos/pmed.0010010.txt
./technical/plos/pmed.0020104.txt
./technical/plos/pmed.0020272.txt
./technical/plos/pmed.0020258.txt
./technical/plos/pmed.0020099.txt
./technical/plos/pmed.0010013.txt
./technical/plos/pmed.0020113.txt
./technical/plos/pmed.0020098.txt
./technical/plos/pmed.0020067.txt
./technical/plos/pmed.0020073.txt
./technical/plos/pmed.0020249.txt
./technical/plos/pmed.0020275.txt
./technical/plos/pmed.0020088.txt
./technical/plos/pmed.0020103.txt
./technical/plos/pmed.0020117.txt
./technical/plos/pmed.0020116.txt
./technical/plos/pmed.0020102.txt
./technical/plos/pmed.0020062.txt
./technical/plos/pmed.0020274.txt
./technical/plos/pmed.0020048.txt
./technical/plos/pmed.0020060.txt
./technical/plos/pmed.0020074.txt
./technical/plos/pmed.0020114.txt
./technical/plos/pmed.0010028.txt
./technical/plos/pmed.0010029.txt
./technical/plos/pmed.0020115.txt
./technical/plos/pmed.0020075.txt
./technical/plos/pmed.0020061.txt
./technical/plos/pmed.0020210.txt
./technical/plos/pmed.0020238.txt
./technical/plos/pmed.0010066.txt
./technical/plos/pmed.0020198.txt
./technical/plos/pmed.0010067.txt
./technical/plos/pmed.0020007.txt
./technical/plos/pmed.0020239.txt
./technical/plos/pmed.0020005.txt
./technical/plos/pmed.0020039.txt
./technical/plos/pmed.0010071.txt
./technical/plos/pmed.0010058.txt
./technical/plos/pmed.0010070.txt
./technical/plos/pmed.0010064.txt
./technical/plos/pmed.0020158.txt
./technical/plos/pmed.0020206.txt
./technical/plos/pmed.0020212.txt
./technical/plos/pmed.0020216.txt
./technical/plos/pmed.0020028.txt
./technical/plos/pmed.0020148.txt
./technical/plos/pmed.0020160.txt
./technical/plos/pmed.0010048.txt
./technical/plos/pmed.0010060.txt
./technical/plos/pmed.0010061.txt
./technical/plos/pmed.0010049.txt
./technical/plos/pmed.0020161.txt
./technical/plos/pmed.0020149.txt
./technical/plos/pmed.0020015.txt
./technical/plos/pmed.0020203.txt
./technical/plos/pmed.0020201.txt
./technical/plos/pmed.0020017.txt
./technical/plos/pmed.0010062.txt
./technical/plos/pmed.0020189.txt
./technical/plos/pmed.0020162.txt
./technical/plos/pmed.0020016.txt
./technical/plos/pmed.0020002.txt
./technical/plos/pmed.0020200.txt
./technical/plos/pmed.0020231.txt
./technical/plos/pmed.0020027.txt
./technical/plos/pmed.0020033.txt
./technical/plos/pmed.0010047.txt
./technical/plos/pmed.0010046.txt
./technical/plos/pmed.0010052.txt
./technical/plos/pmed.0020191.txt
./technical/plos/pmed.0020146.txt
./technical/plos/pmed.0020232.txt
./technical/plos/pmed.0020226.txt
./technical/plos/pmed.0020024.txt
./technical/plos/pmed.0020018.txt
./technical/plos/pmed.0020144.txt
./technical/plos/pmed.0020150.txt
./technical/plos/pmed.0020187.txt
./technical/plos/pmed.0010050.txt
./technical/plos/pmed.0010051.txt
./technical/plos/pmed.0020192.txt
./technical/plos/pmed.0010045.txt
./technical/plos/pmed.0020145.txt
./technical/plos/pmed.0020019.txt
./technical/plos/pmed.0020237.txt
./technical/plos/pmed.0020009.txt
./technical/plos/pmed.0020035.txt
./technical/plos/pmed.0020021.txt
./technical/plos/pmed.0020155.txt
./technical/plos/pmed.0010069.txt
./technical/plos/pmed.0010041.txt
./technical/plos/pmed.0020182.txt
./technical/plos/pmed.0020196.txt
./technical/plos/pmed.0020197.txt
./technical/plos/pmed.0010068.txt
./technical/plos/pmed.0020140.txt
./technical/plos/pmed.0020020.txt
./technical/plos/pmed.0020034.txt
./technical/plos/pmed.0020236.txt
./technical/plos/pmed.0020208.txt
./technical/plos/pmed.0020022.txt
./technical/plos/pmed.0020036.txt
./technical/plos/pmed.0010056.txt
./technical/plos/pmed.0020195.txt
./technical/plos/pmed.0010042.txt
./technical/plos/pmed.0020181.txt
./technical/plos/pmed.0020180.txt
./technical/plos/pmed.0020194.txt
./technical/plos/pmed.0020157.txt
./technical/plos/pmed.0020023.txt
./technical/plos/pmed.0020235.txt
./technical/plos/pmed.0020209.txt
./technical/plos/pmed.0020246.txt
./technical/plos/pmed.0020050.txt
./technical/plos/pmed.0020118.txt
./technical/plos/pmed.0010030.txt
./technical/plos/pmed.0010024.txt
./technical/plos/pmed.0010025.txt
./technical/plos/pmed.0020086.txt
./technical/plos/pmed.0020045.txt
./technical/plos/pmed.0020247.txt
./technical/plos/pmed.0020047.txt
./technical/plos/pmed.0020090.txt
./technical/plos/pmed.0010026.txt
./technical/plos/pmed.0020085.txt
./technical/plos/pmed.0020091.txt
./technical/plos/pmed.0020278.txt
./technical/plos/pmed.0020268.txt
./technical/plos/pmed.0010022.txt
./technical/plos/pmed.0010036.txt
./technical/plos/pmed.0010023.txt
./technical/plos/pmed.0020123.txt
./technical/plos/pmed.0020094.txt
./technical/plos/pmed.0020257.txt
./technical/plos/pmed.0020055.txt
./technical/plos/pmed.0020082.txt
./technical/plos/pmed.0010021.txt
./technical/plos/pmed.0010034.txt
./technical/plos/pmed.0010008.txt
./technical/plos/pmed.0020120.txt
./technical/plos/pmed.0020040.txt
./technical/plos/pmed.0020068.txt
./technical/plos/pmed.0020281.txt
./technical/plos/pmed.0020242.txt
./technical/biomed/gb-2001-2-4-research0010.txt
./technical/biomed/gb-2001-2-4-research0011.txt
./technical/biomed/gb-2002-3-9-research0043.txt
./technical/biomed/gb-2001-2-7-research0025.txt
./technical/biomed/gb-2002-3-7-research0032.txt
./technical/biomed/gb-2001-2-4-research0012.txt
./technical/biomed/gb-2001-2-7-research0024.txt
./technical/biomed/gb-2001-2-3-research0008.txt
./technical/biomed/gb-2002-3-9-research0046.txt
./technical/biomed/gb-2002-3-7-research0037.txt
./technical/biomed/gb-2001-2-8-research0027.txt
./technical/biomed/gb-2001-2-11-research0046.txt
./technical/biomed/gb-2001-2-8-research0032.txt
./technical/biomed/gb-2002-3-7-research0036.txt
./technical/biomed/gb-2002-3-9-research0051.txt
./technical/biomed/gb-2002-3-9-research0045.txt
./technical/biomed/gb-2001-2-8-research0030.txt
./technical/biomed/gb-2001-2-4-research0014.txt
./technical/biomed/gb-2001-2-11-research0045.txt
./technical/biomed/gb-2002-3-7-research0035.txt
./technical/biomed/gb-2001-2-8-research0031.txt
./technical/biomed/gb-2002-3-9-research0044.txt
./technical/biomed/gb-2002-3-2-research0008.txt
./technical/biomed/gb-2002-3-11-research0059.txt
./technical/biomed/gb-2002-3-11-research0065.txt
./technical/biomed/gb-2001-2-10-research0041.txt
./technical/biomed/gb-2002-3-8-research0040.txt
./technical/biomed/gb-2001-2-9-research0035.txt
./technical/biomed/gb-2002-3-12-research0085.txt
./technical/biomed/gb-2002-3-2-research0009.txt
./technical/biomed/gb-2002-3-6-software0001.txt
./technical/biomed/gb-2002-3-12-research0087.txt
./technical/biomed/gb-2002-3-12-research0078.txt
./technical/biomed/gb-2001-2-6-research0018.txt
./technical/biomed/gb-2001-2-9-research0037.txt
./technical/biomed/gb-2001-2-10-research0042.txt
./technical/biomed/gb-2002-3-12-research0079.txt
./technical/biomed/gb-2002-3-12-research0086.txt
./technical/biomed/gb-2002-3-12-research0082.txt
./technical/biomed/gb-2001-2-6-research0021.txt
./technical/biomed/gb-2001-2-6-research0020.txt
./technical/biomed/gb-2002-3-12-research0083.txt
./technical/biomed/gb-2002-3-11-research0062.txt
./technical/biomed/gb-2002-3-11-research0060.txt
./technical/biomed/gb-2002-3-12-research0081.txt
./technical/biomed/gb-2002-3-12-research0080.txt
./technical/biomed/gb-2002-3-11-research0061.txt
./technical/biomed/gb-2002-3-12-research0072.txt
./technical/biomed/gb-2002-3-12-research0071.txt
./technical/biomed/gb-2000-1-1-research002.txt
./technical/biomed/gb-2001-3-1-research0005.txt
./technical/biomed/gb-2002-3-5-research0024.txt
./technical/biomed/gb-2002-3-5-research0025.txt
./technical/biomed/gb-2001-3-1-research0004.txt
./technical/biomed/gb-2001-2-2-research0004.txt
./technical/biomed/gb-2002-3-5-research0021.txt
./technical/biomed/gb-2002-3-5-research0020.txt
./technical/biomed/gb-2001-3-1-research0001.txt
./technical/biomed/gb-2002-3-12-research0075.txt
./technical/biomed/gb-2002-3-12-research0088.txt
./technical/biomed/gb-2002-3-12-research0077.txt
./technical/biomed/gb-2002-3-5-research0022.txt
./technical/biomed/gb-2002-3-5-research0023.txt
./technical/biomed/gb-2002-3-6-research0029.txt
./technical/biomed/gb-2002-3-9-research0049.txt
./technical/biomed/gb-2002-3-9-research0048.txt
./technical/biomed/gb-2002-3-10-research0052.txt
./technical/biomed/gb-2001-2-12-research0055.txt
./technical/biomed/gb-2002-3-4-research0019.txt
./technical/biomed/gb-2002-3-4-research0018.txt
./technical/biomed/gb-2001-2-12-research0054.txt
./technical/biomed/gb-2002-3-10-research0053.txt
./technical/biomed/gb-2002-3-3-research0012.txt
./technical/biomed/gb-2000-1-2-research0003.txt
./technical/biomed/gb-2002-3-8-research0039.txt
./technical/biomed/gb-2001-2-12-research0051.txt
./technical/biomed/gb-2002-3-8-research0038.txt
./technical/biomed/gb-2002-3-10-research0056.txt
./technical/biomed/gb-2002-3-3-research0011.txt
./technical/biomed/gb-2002-3-10-research0054.txt
./technical/biomed/gb-2001-2-12-research0053.txt
./technical/biomed/gb-2001-2-3-research0007.txt
./technical/biomed/gb-2002-3-10-research0055.txt
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-1.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-7.txt
./technical/911report/chapter-9.txt
./technical/911report/chapter-8.txt
./technical/911report/preface.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-10.txt
./technical/911report/chapter-11.txt
```

Example 2: Case-insensitive directory search
```
$ find ./technical -type d -iname "*p*"
```
Output:
![Image](option_iname_directory.png)
This command searches for directories with a case-insensitive match to *p*. This is useful for finding directories when the naming convention is not consistently applied.

Markdown for the Output:
```
./technical/government/Env_Prot_Agen
./technical/government/Alcohol_Problems
./technical/government/Post_Rate_Comm
./technical/plos
./technical/911report
```
### 3. Using the -size option

The -size option allows you to find files of a specific size. This can be useful for locating files that are too large or to identify files that are empty.

Example 1: Finding files less than 1 kilobyte
```
$ find ./technical -type f -size -1k 
```
Output:
![Image](less_than_1kb.png)
This command lists files less than 1 kilobyte. It's useful for identifying large files that may be taking up too much space.

Markdown for the Output:
```
./technical/plos/pmed.0020191.txt
./technical/plos/pmed.0020226.txt
```
Example 2: Finding empty files
```
$ find ./technical -type f -size 0
```
Output:
![Image](emptyfiles.png)
This command finds files that are exactly 0 bytes in size, which often indicates empty files. This can be useful for cleaning up unnecessary files from a directory.

Markdown for the Output:

```
```
outputs nothing

Example 3: Finding directories less than 10 kilobytes
```
find ./technical -type d  -size -10k
```
Output:
![Image](size_directory.png)
This command finds directories less than 10 kilobytes. This can be useful for cleaning up large-size directories.

Markdown for the Output:
```
./technical
./technical/government
./technical/government/About_LSC
./technical/government/Env_Prot_Agen
./technical/government/Alcohol_Problems
./technical/government/Gen_Account_Office
./technical/government/Post_Rate_Comm
./technical/government/Media
./technical/plos
./technical/911report
```

### 4. Using the -mtime option
The -mtime option finds files based on their modification time. This can be useful for locating recently modified files or files that haven't been touched in a long time.

Example 1: Finding files modified in the last 24 hours
```
$ find ./technical -type f -mtime -1
```
Output:
![Image](modified_lessthan_24hours.png)
This command finds files that have been modified in the last 24 hours. It's useful for reviewing recent changes.

Markdown for the Output:
```
./technical/.DS_Store
./technical/911report/chapter-8.txt
```

Example 2: Finding directories not modified in the last 30 days
```
$ find ./technical -type d -mtime +30
```
Output:
![Image](notmodified_last30days.png)
This command lists directories that have not been modified in the last 30 days. This can be helpful for identifying outdated directories that may no longer be needed.

Markdown for the Output:
```
```
outputs nothing
