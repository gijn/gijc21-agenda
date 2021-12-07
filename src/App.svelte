<script>
  import { agenda } from './agenda.js'
  import Icon from './Icon.svelte'
  const speakerList = [...Array(20).keys()]
  const colors = [
    '#a6cee3',
    '#1f78b4',
    '#b2df8a',
    '#33a02c',
    '#fb9a99',
    '#e31a1c',
    '#fdbf6f',
    '#ff7f00',
    '#cab2d6',
    '#6a3d9a',
    '#ffff99',
    '#b15928',
  ]

  agenda.forEach((d) => {
    let speakers = []
    speakerList.forEach((e) => {
      if (d[`speaker_${e}`]) {
        speakers.push(d[`speaker_${e}`])
      }
    })

    d.speakers = speakers
  })

  function trackStyle(t) {
    if (t.toLowerCase() === 'none') return '#000'
    else if (t.toLowerCase() === 'environment') return colors[0]
    else if (t.toLowerCase() === 'data') return colors[1]
    else if (t.toLowerCase() === 'health') return colors[2]
    else if (t.toLowerCase() === 'corruption') return colors[3]
    else if (t.toLowerCase() === 'broadcast') return colors[4]
    else if (t.toLowerCase() === 'workshop') return colors[5]
    else if (t.toLowerCase() === 'panel') return colors[6]
    else if (t.toLowerCase() === 'security') return colors[7]
    else if (t.toLowerCase() === 'networking') return colors[8]
    else {
      return 'red'
    }
  }
</script>

<main>
  {#each agenda as a}
    <div class="card">
      <div class="track" style="background: {trackStyle(a.track)};">
        {a.track_name}
      </div>
      <div class="card-inner">
        <div class="session">{a.session}</div>
        <div class="speakers">
          {#each a.speakers as speaker}
            <div class="speaker">
              {speaker}
            </div>
          {/each}
        </div>
        <div class="meta">
          <Icon name="clock" />
          <div class="meta-small">{a.duration} minutes &nbsp;</div>
          <Icon name="video" />
        </div>
      </div>
    </div>
  {/each}
</main>

<style>
  .card {
    width: 400px;
    /* padding: 20px; */
    border: solid 1px lightgray;
    background: #fff;
    margin: 10px;
    font-family: 'Roboto Condensed', Arial, Helvetica, sans-serif;
    -webkit-box-shadow: 1px 1px 5px 0px rgba(0, 0, 0, 0.31);
    -moz-box-shadow: 1px 1px 5px 0px rgba(0, 0, 0, 0.31);
    box-shadow: 1px 1px 5px 0px rgba(0, 0, 0, 0.31);
  }
  .card-inner {
    padding: 10px;
  }
  .track {
    padding: 5px 10px;
    background: dodgerblue;
    font-size: 0.8rem;
    text-transform: uppercase;
    color: #fff;
  }
  .session {
    font-weight: 700;
    text-transform: uppercase;
    font-size: 1.2rem;
    color: #004c6b;
    margin-bottom: 10px;
  }
  .speakers {
    display: grid;
    grid-template-columns: 1fr 1fr;
  }
  .speaker {
    margin-top: 5px;
    margin-bottom: 5px;
    font-weight: 500;
    font-size: 1.2rem;
  }
  .meta {
    margin-top: 10px;
    font-size: 1rem;
    text-transform: uppercase;
  }
  .meta-small {
    font-size: 0.8rem;
    display: inline-block;
    transform: translate(0px, -3px);
  }
</style>
