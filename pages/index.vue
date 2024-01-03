<template>
  <div class="container">
    <div class="stats">
      <h1>A stats/memory tracker of my time at inVentiv Health/Syneos Health</h1>
      <p>In the {{ totalTenure }} that I've been at GSW, there have been a lot of moments. Here are some of the highlights.</p>
      <ul>
        <li>Started on {{ titles[0].start }}, as a {{ titles[0].title }} for {{ titles[0].company }}.</li>
        <li>Since then I've held {{ titlesCount }} different titles.</li>
        <li>Currently I am the {{ titles[4].title }} for {{ titles[4].company }}</li>
        <li>Been a part of 4 different groups/hubs/offices: inVentiv Creative Studios / GSW Philadelphia / GSW New York / GSW Columbus.</li>
        <li>Sat at {{ desks }} desks in {{ officeSpaces }} different office spaces ({{ homeDesks }} of which were home offices).</li>
        <li>Seen {{ mergers }} merger(s) and {{ acquisitions }} acquisition(s).</li>
        <li>Worked under {{ bosses }} different bosses.</li>
        <li>Had {{ managingDirectors }} managing directors.</li>
        <li>Led over {{ developerCount }} developers.</li>
        <li>Launched and maintained over <strong>{{ websitesCount }}</strong> websites, <strong>{{ ivaCount }}</strong> iVAs (Veeva CLM Presentations) and <strong>{{ confPanelCount }}</strong> interactive conference panels.*<sup>&dagger;</sup></li>
        <li>Attended {{ conferenceCount }} conferences.<sup>&Dagger;</sup></li>
        <li>Achieved {{ certificationCount }} certifications.</li>
        <li>Had {{ children }} kids.</li>
        <li>There have been {{ usaPresidents }} US Presidents.</li>
        <li
          v-if="pandemicCount === 1"
        >
          There was {{ pandemicCount }} pandemic (
          <span
            v-for="(pandemic, index) in pandemics"
            :key="index"
          >
            {{ pandemic }}
          </span>
          )
        </li>
        <li
          v-else
        >
          There were {{ pandemicCount }} pandemics (
          <span
            v-for="(pandemic, index) in pandemics"
            :key="index"
          >
            {{ pandemic }},
          </span>
          ).
        </li>
      </ul>
      <!-- TODO: Something Cool -->
      <!-- Create AR marker and display on website
      Provide instructions to view website on phone
      Either use the AR marker displayed on website, OR print out marker (provide download)
      AR Headshot with contact information -->
      <p
        class="footnote"
      >
        *I didn't bother to start tracking everything until my 5th year at GSW, so I'm sure I'm forgetting projects.
      </p>
      <p
        class="footnote"
      >
        <sup>&dagger;</sup>I'm not including emails, banners, or internal tools that make every day life easier.
      </p>
      <p
        class="footnote"
      >
        <sup>&Dagger;</sup>I attend virtual congresses pretty regularly, I'm sure this number isn't accounting for every one.
      </p>

      <div class="contact-information">
        <h2>Contact Information</h2>
        <p><strong>Email:</strong> brandon [at] morsecodemedia [dot] com</p>
        <p><strong>Website:</strong> <a href="https://www.morsecodemedia.com/" target="_blank">www.morsecodemedia.com</a></p>
        <p><strong>Blog:</strong> <a href="https://blog.morsecodemedia.com/" target="_blank">blog.morsecodemedia.com</a></p>
        <p><strong>Github:</strong> <a href="https://github.com/morsecodemedia" target="_blank">morsecodemedia</a></p>
        <p><strong>LinkedIn:</strong> <a href="https://www.linkedin.com/in/brandonmorse/" target="_blank">linkedin.com/brandonmorse</a></p>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment'

export default {
  data () {
    return {
      desks: 15,
      homeDesks: 4,
      officeSpaces: 4, // State Street, Brandywine 1st floor (Dev Separate), Brandywine 1st (Together), Brandywine 2nd Floor
      homeOffices: 4, // 143 3rd Floor, 143 Basement, 35 1st Floor, 35 2nd Floor
      companies: 2, // iCS, GSW
      mergers: 3, // Navicor Philly->GSW Newtow (GSW Philly), GSW Philly->GSW NYC (GSW EAST), Spherico CBUS->GSW CBUS
      acquisitions: 2, // INC/inVentiv->Syneos, VC takes over Syneos goes Private
      managingDirectors: 9, // Lynn Dinsmore, Melissa Marrow, Sam C, Jon Nelson, Nancy Finer, Chris Mizek, Sonja Foster-Storch, Andrew Schirmer, Jen Oleski
      companyPresidents: 4, // Marcy, Sunny, JD,
      bosses: 4, // Jay Karr, James Tomasino, Sam Cannizzaro, Bryan Roman
      children: 2,
      pitches: 3, // Dysport Connect, AZ Accessibility, Genicos > Odyssey TX,
      pitchesWon: 1,
      titlesLength: 0,
      websites: [
        'belbuca hcp (Endo > Belbuca)',
        'belbuca patient (Endo > Belbuca)',
        'supprelin la patient (Endo > Supprelin LA)',
        'supprelin la hcp (Endo > Supprelin LA)',
        'spritam hcp (Aprecia > Spritam)',
        'spritam patient (Aprecia > Spritam)',
        'radicavahcp.com (MTPA > Radicava)',
        'radicava.com (MTPA > Radicava)',
        'xiaflex dc hcp (Endo > Xiaflex DC)',
        'xiaflex dc patient (Endo > Xiaflex DC)',
        'xiaflex pd hcp (Endo > Xiaflex PD)',
        'xiaflex pd patient (Endo > Xiaflex PD)',
        'endomenshealth.com (Endo > Mens Health)',
        'stendrahcp.com (Metuchen > Stendra)',
        'stendra.com (Metuchen > Stendra)',
        'hqblitz.com (MTPA)',
        'api.hqblitz.com (MTPA)',
        'xtra kickstarts (Endo > Xiaflex DC)',
        'axid.com (Amneal > Axid)',
        'unithroidhcp.com (Amneal > Unithroid)',
        'unithroid.com (Amneal > Unithroid)',
        'vitrisa corp (Virtrisa)',
        'legend bio corp (Legend Biopharma)',
        'aveed patient (Endo > Aveed)',
        'aveed hcp (Endo > Aveed)',
        'alswebinars.com (MTPA > ALS Pathways - Radicava DSE)',
        'radicavawebinar.com (MTPA > Radicava)',
        'knownk.com (Dompe > Oxervate DSE)',
        'oxervate.com/hcp (Dompe > Oxervate)',
        'oxervate.com/ (Dompe > Oxervate)',
        'moors clinical trials (Janssen > Esketimine)',
        'lialda 10 year (Shire > Lialda)',
        'built for me (Sunovian)',
        'airduo hcp (Teva > Airduo)',
        'armonair hcp (Teva > ArmonAir)',
        'qvar hcp (Teva > QVAR)',
        'truximahcp.com (Teva > Truxima)',
        'tevacore.com (Teva)',
        'donttakevat.com (Thera)',
        'natesto.com (Acerus > Natesto)',
        'natestohcp.com (Acerus > Natesto)',
        'exservanhcp.com (MTPA > Exservan)',
        'plenitykitchen.com (virtual booth - Gelesis > Plenity)',
        'api.radicavacarelocator.com (API - MTPA > Radicava)',
        'api.hqblitz.com (API - MTPA)',
        'api.natesto.com (API - Acerus > Natesto)',
        'amgencongresses.com (Amgen > Virtual Congresses Platform)',
        'amjevita.com (Amgen > Amjevita)',
        'amjevitapro.com (Amgen > Amjevita)',
        'amgensupportplus.com 1.0 (Amgen)',
        'amgensupportplus.com 2.0 (Amgen)',
        // 'amgensupportplus.com 3.0 (Amgen)',
        // 'omeras yartelmea ves site', ON HOLD
        // 'omeras dse ves site', ON HOLD
        'gastriccancerbiomarkers.com US (Astellas > Zolbe)',
        'gastriccancerbiomarkers.com GLOBAL (Astellas > Zolbe)',
        'zolbe hcp US (Astellas > Vyloy/Zolbe)',
        'zolbe hcp GLOBAL (Astellas > Vyloy/Zolbe)',
        'cuvitruhcp.com (Takeda > Cuvitru)',
        'cuvitru.com (Takeda > Cuvitru)',
        'hyqvia.com (Takeda > HyQvia PI only)',
        'hyqviahcp.com (Takeda > HyQvia PI only)',
        'hyqvia.com (Takeda > HyQvia PI PEDs)',
        'hyqviahcp.com (Takeda > HyQvia PI PEDs)',
        'hyqviacidp.com (Takeda > HyQvia > CIDP Day 0/1)','
        'hyqviacidp.com/hcp (Takeda > HyQvia > CIDP Day 0/1)','
        // 'hyqviahcp.com (Takeda > HyQvia PI/CIDP Indications)', Q1 2024
        // 'hyqvia.com (Takeda > HyQvia PI/CIDP Indications)', Q1 2024
        // 'IDN Site (Takeda > PDT)', (q4 2023)
        // 'glassialiquid.com' (Takeda > Glassia),
        // 'glassialiquid.com/hcp (Takeda > Glassia)',
        // 'gammagard.com/hcp (Takeda > Gammagard)',
        // 'gammagard.com (Takeda > Gammagard)'
        'api.dysport.com (API - Ipsen Dysport Specialist Locator)',
        'dysport.com (Ipsen > Dysport)',
        'dysporthcp.com (Ipsen > Dysport)',
        'omeros.com (Omeros Corporate)',
        'eisthreat.com (Omeros)',
        // 'yartelmea.com (Omeros > Yartelmea)',
        'cuseemewisondisease.com (Alexion > Wilson Disease DSE)',
        'SeroquelXR.com (AZ > Seroquel)',
        'Forxiga - The Meryl Experience (AZ > Forxiga)',
        'amgenassist.com (Amgen > AmgenAssist)',
        'oxervate.com (Dompe > Oxervate)',
        'amjevita.com (Amgen > Amjevita)',
        'amjevitapro.com (Amgen > Amjevita)',
        'lillyloxooncologypipeline.com (Lilly > Loxo)',
        // 'lillyloxooncologypipeline.com Phase 2 (Lilly > Loxo)',
        'saluda.com (Saluda Medical > Evoke)',
        'regenerononcmedicalbooth.com (ASH 2021 Hematology Pipeline - Regeneron)',
        'regenerononcmedicalbooth.com (EHA 2022 Hematology Pipeline - Regeneron)',
        'regennerononcmedicabooth.com (ASCO 2022 Oncology Pipeline - Regeneron)',
        'oncology.regennerononcmedicabooth.com (ESMO 2022 Oncology Pipeline - Regeneron)',
        'hematology.regennerononcmedicabooth.com (ESMO 2022 Hematology Pipeline - Regeneron)',
        'oncology.regennerononcmedicabooth.com (ASH 2022 Oncology Pipeline - Regeneron)',
        'hematology.regennerononcmedicabooth.com (ASH 2022 Hematology Pipeline - Regeneron)',
        'vonjo.com (CTI > Vonjo)',
        'vonjo.com/hcp (CTI > Vonjo)',
        'Roche Alz OWP',
        'Roche Cobas Pure Marketo',
        'Roche MD5800 OWP',
        'Roche MD5800 Marketo',
        'askLia.ca (Amgen Canada > Prolia)',
        'evenity.ca (Amgen Canada > Evenity)',
        'evenity.ca/hcp (Amgen Canada > Evenity)',
        'boneattackinosteoporosis.ca (Amgen Canada > ?)',  
        'Quest Diagnostics PCP AEM Landing Page (QD > PCP)',
        'Quest Diagnostics AD Detect AEM Landing Page (QD > Ad-Detect)',
        // 'Aranesp Neph Hub (Amgen > Aranesp)',
        // 'Spherico Agency Site (Syneos > Spherico)',
        // 'GSW Agency Site (Syneos > GSW)',
        'Gilead Cloud Page (Gilead > ?)',
        // nexlizethcp.com'(Esperion > Nexlizet/Nexletol)',
        // nexlizet.com (Esperion > Nexlizet/Nexletol),
        // Ozempic Unbranded Canada Site,
        // Vyvanse HCP Canada Site,
        // Vyvanse Patient Canada Site,
        // Vyvanse Unbranded Canada Site,
        'newheartvalve.com/ (Edwards > TAVR)',
        'edwards.com/ (Edwards)',
      ],
      ivas: [
        'mtpa human body en-us',
        'mtpa human body fr-ca',
        'mtpa human body en-ca',
        'radicava main',
        'celgene r2',
        'endo xpd pd exchange',
        'aerie rocklatan v1',
        'aerie rhopressa v1',
        'aerie rocklatan v2',
        'aerie rhopressa v2',
        'aerie rocklatan v3',
        'aerie rhopressa v3',
        'mtpa radicava main',
        'shire vyvanse adha',
        'shire mydayis',
        'acerus natesto',
        'agile twirla main',
        'agile twirla resource library',
        'j&j zyrtec',
        'j&j aveeno',
        'shire lialda 10yr',
        'shire lialda main',
        'mtpa radicava aan',
        'mtpa radicava hcp guide',
        'mtpa radicava mode of infusion',
        'mtpa radicava patient profiles',
        'mtpa radicava video library',
        'aerie formulary tool',
        'aerie myinsights dashboard',
        'mtpa radicava access coverage',
        'thera egrifta main',
        'thera egrifta unbranded vat',
        'shire vyvanse access and affordability',
        'iber bms beam',
        'aerie dynamic formulaerie tool',
        'gelesis plenity main v1.0',
        'gelesis plenity main v1.1',
        'gelesis plenity main v1.2',
        'gelesis plenity talking paper v1.0',
        'gelesis plenity talking paper v1.1',
        'gelesis plenity talking paper v1.2',
        'ipsen dysport multi-indication v1.0',
        'ipsen dysport multi-indication v1.1',
        'ipsen dysport multi-indication v2.0 - framework overhaul',
        // 'ipsen dysport multi-indication v2.1',
        'takeda hyqvia main',
        'takeda cuvitru main',
        'takeda cuvitru needlestick calculator',
        'You Can Do That In Veeva? Presentation',
        'CTI Bone On Fire Veeva'
      ],
      confPanels: [
        'rad 1',
        'rad 2',
        'rad 3',
        'rad 4',
        'shire 1',
        'xdc 1',
        'xdc 2',
        'xdc 3',
        'xpd 1',
        'edex 1',
        'valstar 1',
        'aveed 1',
        'testopel 1',
        'emh 1',
        'xpd 2',
        'xpd 3',
        'omeros dse interactive brochure',
        'regenerononcmedicalbooth.com (ASH 2021 Hematology Pipeline - Regeneron)',
        'regenerononcmedicalbooth.com (EHA 2022 Hematology Pipeline - Regeneron)',
        'regennerononcmedicabooth.com (ASCO 2022 Oncology Pipeline - Regeneron)',
        'oncology.regennerononcmedicabooth.com (ESMO 2022 Oncology Pipeline - Regeneron)',
        'hematology.regennerononcmedicabooth.com (ESMO 2022 Hematology Pipeline - Regeneron)',
        'oncology.regennerononcmedicabooth.com (ASH 2022 Oncology Pipeline - Regeneron)',
        'hematology.regennerononcmedicabooth.com (ASH 2022 Hematology Pipeline - Regeneron)',
        'omeros eisthreat.com panel',
        'omeros moa video panel',
        'CTI Bone on Fire Dreamoc',
        'The Art of Healing > Lilly Paint By Numbers',
        // 'Vyloy Branded HCP'
      ],
      titles: [
        {
          company: 'inVentiv Creative Studios',
          location: 'Newtown, PA',
          title: 'Technology Manager',
          start: '2015-10-12',
          end: '2016-02-01'
        },
        {
          company: 'GSW Advertising',
          location: 'Newtown, PA',
          title: 'Associate Technology Director',
          start: '2016-02-01',
          end: '2018-01-01'
        },
        {
          company: 'GSW Advertising',
          location: 'Newtown, PA',
          title: 'Lead Architect',
          start: '2018-01-01',
          end: '2019-06-28'
        },
        {
          company: 'GSW Advertising',
          location: 'Newtown, PA/New York, NY',
          title: 'Technology Director',
          start: '2019-06-28',
          end: '2021-12-13'
        },
        {
          company: 'GSW Advertising',
          location: 'Remote/GSW Columbus',
          title: 'VP Technology Director, Creative Technology',
          start: '2021-12-13',
          end: ''
        }
      ],
      developers: [
        'James Tomasino',
        'Ankur',
        'Juan Vasquez',
        'Dilip Lama',
        'Aiden Muneath',
        'Thaw Htaik',
        'Steve (real estate dude)',
        'Steve McDonald',
        'Padma',
        'Lou',
        'Charlie',
        'Sheetal',
        'Neema',
        'Steph Mitterko',
        'Rich Mccaulsky-Clarke',
        'Mike Halat',
        'Mike K',
        'Lance',
        'Bill Condo',
        'Jason Pan',
        'Todd Juro',
        'Zach Kramer',
        'Greg V',
        'Fiana G',
        'Amulya',
        'Ted Moke',
        'Anthony Clever',
        'Vinny Di Cairano',
        'Greg Jaspen',
        'Max Currier',
        'Lan Zhang',
        'Mickey de Lorenzo',
        'Scott Ellison',
        'James C',
        'Jason Sankey',
        'Brandon Diaz',
        'Jerrold Smith',
        'Chris Miller',
        'Andrea',
        'Jason Feldheim'
      ],
      conferences: [
        {
          name: 'Veeva Summit',
          year: '2017'
        },
        {
          name: 'AWS Summit NYC',
          year: '2016'
        },
        {
          name: 'AWS Summit NYC',
          year: '2017'
        },
        {
          name: 'AWS Summit NYC',
          year: '2018'
        },
        {
          name: 'VueConf.us',
          year: '2018'
        },
        {
          name: 'Connect.tech',
          year: '2020'
        },
        {
          name: 'VueConf Toronto',
          year: '2020'
        },
        {
          name: 'Pluralsight LIVE',
          year: '2020'
        },
        {
          name: 'JAMStack Conf',
          year: '2020'
        },
        {
          name: 'Headless Commerce Summit',
          year: '2020'
        },
        {
          name: 'Alexa Live',
          year: '2020'
        },
        {
          name: 'Litmus Live',
          year: '2020'
        },
        {
          name: 'AWS Summit Americas',
          year: '2020'
        },
        {
          name: 'AWS:reInvent',
          year: '2020'
        },
        {
          name: 'GitLab Commit',
          year: '2021'
        },
        {
          name: 'Nuxt Nation',
          year: '2021'
        },
        {
          name: 'Vue Nation',
          year: '2021'
        },
        {
          name: 'Nuxt Nation',
          year: '2022'
        }

      ],
      certifications: [
        {
          certification: 'Engage for Portals Technical Certification',
          organization: 'Veeva Systems',
          organizationLogo: '',
          certificationStart: 'January 2023',
          certificationEnd: 'January 2024'
        },
        {
          certification: 'Engage for Portals Business Certification',
          organization: 'Veeva Systems',
          organizationLogo: '',
          certificationStart: 'January 2023',
          certificationEnd: 'January 2024'
        },
        {
          certification: 'Engage Technical Certification',
          organization: 'Veeva Systems',
          organizationLogo: '',
          certificationStart: 'January 2023',
          certificationEnd: 'January 2024'
        },
        {
          certification: 'Engage Business Certification',
          organization: 'Veeva Systems',
          organizationLogo: '',
          certificationStart: 'January 2023',
          certificationEnd: 'January 2024'
        },
        {
          certification: 'Approved Email Business Certification',
          organization: 'Veeva Systems',
          organizationLogo: '',
          certificationStart: 'January 2023',
          certificationEnd: 'January 2024'
        },
        {
          certification: 'Approved Email Technical Certification',
          organization: 'Veeva Systems',
          organizationLogo: '',
          certificationStart: 'April 2022',
          certificationEnd: 'April 2023'
        },
        {
          certification: 'CLM Technical Certification',
          organization: 'Veeva Systems',
          organizationLogo: '',
          certificationStart: 'January 2023',
          certificationEnd: 'January 2024'
        },
        {
          certification: 'CLM Business Certification',
          organization: 'Veeva Systems',
          organizationLogo: '',
          certificationStart: 'January 2023',
          certificationEnd: 'January 2024'
        },
        {
          certification: 'Approved Email Technical Certification',
          organization: 'Veeva Systems',
          organizationLogo: '',
          certificationStart: 'April 2022',
          certificationEnd: 'April 2023'
        },
        {
          certification: 'Certified Professional in Accessibility Core Competencies (CPACC)',
          organization: 'IAAP',
          organizationLogo: '',
          certificationStart: 'October 2020',
          certificationEnd: 'October 2023'
        },
        {
          certification: 'CLM Technical Certification',
          organization: 'Veeva Systems',
          organizationLogo: '',
          certificationStart: 'September 2020',
          certificationEnd: 'September 2021'
        },
        {
          certification: 'Digital Marketing Analytics',
          organization: 'MIT Sloan School of Management',
          organizationLogo: '',
          certificationStart: 'August 2019',
          certificationEnd: ''
        },
        {
          certification: 'AWS Certified ALexa Skill Builder - Specialty',
          organization: 'Amazon Web Services',
          organizationLogo: '',
          certificationStart: 'January 2019',
          certificationEnd: 'January 2022'
        },
        {
          certification: 'Custom Lightbox Ads Badge Certification',
          organization: 'DoubleClick',
          organizationLogo: '',
          certificationStart: 'March 2016',
          certificationEnd: ''
        },
        {
          certification: 'Dynamic Creative Badge Certification',
          organization: 'DoubleClick',
          organizationLogo: '',
          certificationStart: 'March 2016',
          certificationEnd: ''
        },
        {
          certification: 'VPAID Badge Certification',
          organization: 'DoubleClick',
          organizationLogo: '',
          certificationStart: 'March 2016',
          certificationEnd: ''
        },
        {
          certification: 'YouTube Masthead Badge Certification',
          organization: 'DoubleClick',
          organizationLogo: '',
          certificationStart: 'March 2016',
          certificationEnd: ''
        },
        {
          certification: 'HTML5 Studio Certification',
          organization: 'DoubleClick',
          organizationLogo: '',
          certificationStart: 'February 2016',
          certificationEnd: ''
        },
        {
          certification: 'Veeva MyInsights',
          organization: 'Veeva Systems',
          organizationLogo: '',
          certificationStart: 'May 2017',
          certificationEnd: 'May 2018'
        }
      ],
      pandemics: [
        'COVID-19'
      ],
      quarantine: 19,
      usaPresidents: 3
    }
  },
  computed: {
    pitchWinPercentage () {
      const calc = this.pitches / this.pitchesWon
      if (typeof calc === 'number' && calc !== Infinity) {
        return calc
      } else {
        return 0
      }
    },
    websitesCount () {
      return this.websites.length
    },
    ivaCount () {
      return this.ivas.length
    },
    confPanelCount () {
      return this.confPanels.length
    },
    pandemicCount () {
      return this.pandemics.length
    },
    conferenceCount () {
      return this.conferences.length
    },
    certificationCount () {
      return this.certifications.length
    },
    developerCount () {
      return this.developers.length
    },
    titlesCount () {
      return this.titles.length
    },
    titlesLength () {
      this.titlesLength = this.titles.length
    },
    startTenure () {
      return new Date(this.titles[0].start)
    },
    endTenure () {
      if (this.titles[this.titlesCount - 1].end === '') {
        return new Date()
      } else {
        return new Date(this.titles[this.titlesCount - 1].end)
      }
    },
    totalTenure () {
      const startDate = moment(this.startTenure)
      const endDate = moment(this.endTenure)

      let totalTenure = moment.duration(startDate.diff(endDate))
      const years = totalTenure._data.years.toString().replace(/-/g, '')
      const months = totalTenure._data.months.toString().replace(/-/g, '')
      const days = totalTenure._data.days.toString().replace(/-/g, '')

      totalTenure = years + ' years, ' + months + ' months, and ' + days + ' days'

      return totalTenure
    }
  },
  methods: {
    tenure: (startDate, endDate) => {
      const time = (endDate.getTime() - startDate.getTime()) / 1000
      const year = Math.abs(Math.round((time / (60 * 60 * 24)) / 365.25))
      const month = Math.abs(Math.round(time / (60 * 60 * 24 * 7 * 4)))
      const days = Math.abs(Math.round(time / (3600 * 24)))
      return year + ' years, ' + month + ' months, or ' + days + ' days'
    }
  }
}
</script>

<style>
body {
  color: #35495e;
  font-size: 20px;
  font-weight: 300;
}

.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: left;
  padding: 20px 30px;
}

h1 {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

h2 {
  font-weight: 300;
  font-size: 36px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

p {
  margin-bottom: 15px;
}

p.footnote {
  font-size: 14px;
}

ul {
  margin: 0 0 0 -20px;
}

ul li {
  margin-bottom: 15px;
}

</style>
