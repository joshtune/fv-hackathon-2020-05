<script>
  let count = 0;
  let documentCollection = [];

  function add() {
    count = count + 1;
    documentCollection = documentCollection.concat({
      id: count,
      file: null,
      description: ''
    });
  }

  function remove(document) {
    documentCollection = documentCollection.filter(doc => doc.id !== document.id);
    count = documentCollection.length;
  }

  function reset() {
    documentCollection = [];
    count = 0;
  }

  function upload() {
    let data = new FormData();
    documentCollection.forEach(doc => data.append(`doc-${doc.id}`, doc));
    fetch('/upload/docs', {method: 'POST', body: data});
  }
</script>

<button on:click={add}>Add</button>
<button on:click={reset}>Reset</button>
<button on:click={upload} disabled={documentCollection.length === 0}>Upload</button>
<button>{count}</button>

{#if documentCollection.length > 0}
  {#each documentCollection as doc}
    <div class="document">
      <label for="document-description-{doc.id}">Description:</label>
      <input
        type="text"
        id="document-description-{doc.id}"
        bind:value={doc.description} />

      <label for="document-file-{doc.id}">Upload:</label>
      <input
        bind:value={doc.file}
        id="document-file-{doc.id}"
        name="document-file-{doc.id}"
        type="file"
      />
      <button on:click={remove(doc)}>Remove</button>
    </div>
  {/each}
{/if}

<style>
  .document { border: 1px solid #cccccc; padding: 15px; margin-bottom: 10px; }
  input { display: block; width: 100%; }
</style>
