<script context="module">
  export const load = async ({ fetch, params }) => {
    const res = await fetch(`/utstillinger/${params.id}.json`);

    if (res.ok) {
      const contest = await res.json();
      if (contest.maleCertDogRef) {
        contest.maleCertDogRef = contest.maleCertDogRef["@ref"].id;
      }
      if (contest.femaleCertDogRef) {
        contest.femaleCertDogRef = contest.femaleCertDogRef["@ref"].id;
      }
      if (contest.maleNordCertDogRef) {
        contest.maleNordCertDogRef = contest.maleNordCertDogRef["@ref"].id;
      }
      if (contest.femaleNordCertDogRef) {
        contest.femaleNordCertDogRef = contest.femaleNordCertDogRef["@ref"].id;
      }
      return {
        props: { contest },
      };
    }

    return {
      status: res.status,
      error: res.error,
    };
  };
</script>

<script>
  export let contest;

  function getDogNameByDogId(dogId) {
    for (let result of contest.results) {
      if (result.dogId === dogId) {
        return result.dogName;
      }
    }
  }
</script>

<h1>{contest.name}</h1>

<div class="contest-info">
  <p style="grid-column: span 2;">{contest.date}, {contest.location}</p>
  <p>Arrangør:</p>
  <p>{contest.host}</p>
  <p>Hunder:</p>
  <p>{contest.numberOfDogs}</p>
  <p>Dommer:</p>
  <p>{contest.judge}</p>
</div>

<div class="shadow-box" style="max-width: 100%; margin-top: 1rem;">
  <h2>Resultater</h2>
  {#if contest.results?.length}
    <p style="margin: 0.5rem 0">
      {contest.pointsByNumDogs} tilleggspoeng fra antall deltagende hunder for toppresultater
    </p>

    {#if contest.maleCertDogRef || contest.femaleCertDogRef || contest.maleNordCertDogRef || contest.femaleNordCertDogRef}
      {#if contest.maleCertDogRef || contest.femaleCertDogRef}
        <div style="margin: 1rem 0 2rem 0;">
          <h3>Cert</h3>
          {#if contest.maleCertDogRef}
            <p style="margin-top: 0.5rem;">
              Hannhund:
              <a href={`/hunder/${contest.maleCertDogRef}`}>
                {getDogNameByDogId(contest.maleCertDogRef)}
              </a>
            </p>
          {/if}
          {#if contest.femaleCertDogRef}
            <p style="margin-top: 0.5rem;">
              Tispe:
              <a href={`/hunder/${contest.femaleCertDogRef}`}>
                {getDogNameByDogId(contest.femaleCertDogRef)}
              </a>
            </p>
          {/if}
        </div>
      {/if}

      {#if contest.maleNordCertDogRef || contest.femaleNordCertDogRef}
        <div style="margin: 1rem 0 2rem 0;">
          <h3>Nord cert</h3>
          {#if contest.maleNordCertDogRef}
            <p style="margin-top: 0.5rem;">
              Hannhund:
              <a href={`/hunder/${contest.maleNordCertDogRef}`}>
                {getDogNameByDogId(contest.maleNordCertDogRef)}
              </a>
            </p>
          {/if}
          {#if contest.femaleNordCertDogRef}
            <p style="margin-top: 0.5rem;">
              Tispe:
              <a href={`/hunder/${contest.femaleNordCertDogRef}`}>
                {getDogNameByDogId(contest.femaleNordCertDogRef)}
              </a>
            </p>
          {/if}
        </div>
      {/if}

      <h3>Premieringer</h3>
    {/if}

    <table>
      <thead>
        <tr>
          <th>Hund</th>
          <th>Resultat</th>
          <th>Poeng</th>
        </tr>
      </thead>
      <tbody>
        {#each contest.results as result}
          <tr>
            <td>
              <a href={`/hunder/${result.dogId}`}>
                {result.dogName}
              </a>
            </td>
            <td>{result.combinedResult}</td>
            <td>{result.points}</td>
          </tr>
        {/each}
      </tbody>
    </table>
  {:else}
    Ingen resultater enda
  {/if}
</div>

<style>
  h1 {
    margin-bottom: 1rem;
  }
  table,
  div {
    width: fit-content;
  }
  .contest-info {
    display: grid;
    grid-template-columns: auto auto;
    gap: 0.5rem;
  }
</style>
