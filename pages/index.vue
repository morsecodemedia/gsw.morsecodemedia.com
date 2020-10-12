<template>
  <div class="container">
    <div class="stats">
      <h1>A stats/memory tracker of my time at GSW</h1>
      <p>In the {{ totalTenure }} that I've been at GSW, there have been a lot of moments. Here are some of the highlights.</p>
      <ul>
        <li>Started on {{ titles[0].start }}, as a {{ titles[0].title }} for {{ titles[0].company }}. Since then I've held {{ titlesCount }} different titles.</li>
        <li>Sat at {{ desks }} desks in {{ officeSpaces }} different office spaces ({{ homeDesks }} of which were home offices).</li>
        <li>Seen {{ mergers }} merger(s) and {{ acquisitions }} acquisition(s).</li>
        <li>Worked under {{ bosses }} different bosses.</li>
        <li>Had {{ managingDirectors }} managing directors.</li>
        <li
          v-if="pitchWinPercentage > 0"
        >
          Was a part of {{ pitches }} pitch(es) with a win percentage of {{ pitchWinPercentage }}%
        </li>
        <li>Had {{ developerCount }} developers report into me at one point in time.</li>
        <li>Had {{ children }} kids.</li>
        <li>Attended {{ conferenceCount }} conferences.</li>
        <li>Achieved {{ certificationCount }} certifications.</li>
        <li>Launched over {{ websitesCount }} websites.</li>
        <li
          v-if="pandemicCount === 1"
        >
          Survived {{ pandemicCount }} pandemic (
          <span
            v-for="(pandemic, index) in pandemics"
            :key="index"
          >
            {{ pandemic }}
          </span>
          )...and {{ quarantine }} months in quarantine.*
        </li>
        <li
          v-else
        >
          Survived {{ pandemicCount }} pandemics (
          <span
            v-for="(pandemic, index) in pandemics"
            :key="index"
          >
            {{ pandemic }},
          </span>
          ).
        </li>
        <li>There have been {{ usaPresidents }} US Presidents.</li>
      </ul>
      <!-- TODO: Something Cool -->
      <!-- Create AR marker and display on website
      Provide instructions to view website on phone
      Either use the AR marker displayed on website, OR print out marker (provide download)
      AR Headshot with contact information -->
      <p
        class="footnote"
      >
        *Assumes that I didn't go back into the office from March 2020 - January 2021.
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
      desks: 14,
      homeDesks: 3,
      officeSpaces: 7,
      homeOffices: 3,
      companies: 2,
      mergers: 1,
      acquisitions: 1,
      managingDirectors: 5,
      companyPresidents: 4,
      bosses: 3,
      children: 2,
      pitches: 1,
      pitchesWon: 0,
      websites: [
        'belbuca hcp',
        'belbuca patient',
        'supprelin la patient',
        'supprelin la hcp',
        'spritam hcp',
        'spritam patient',
        'radicava hcp',
        'radicava patient',
        'xiaflex dc hcp',
        'xiaflex dc patient',
        'xiaflex pd hcp',
        'xiaflex pd patient',
        'endo mens health',
        'stendra hcp',
        'stendra patient',
        'hqblitz',
        'xtra kickstarts',
        'axid hcp',
        'unithroid hcp',
        'unithroid patient',
        'vitrisa corp',
        'legend bio corp',
        'aveed patient',
        'aveed hcp',
        'radicava webinar unbranded',
        'radicava webinar branded',
        'dompe dse',
        'moors clinical trials',
        'lialda 10 year',
        'built for me',
        'airduo',
        'armonair',
        'qvar',
        'dont take vat'
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
          location: 'Newtown, PA',
          title: 'Technology Director',
          start: '2019-06-28',
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
        'Mike Halat',
        'Mike K',
        'Lance',
        'Bill Condo',
        'Jason Pan',
        'Todd Juro',
        'Zach Kramer',
        'Greg V',
        'Fiana',
        'Amulya',
        'Ted Moke',
        'Anthony Clever'
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
        }

      ],
      certifications: [
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
      quarantine: 10,
      usaPresidents: 2
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
