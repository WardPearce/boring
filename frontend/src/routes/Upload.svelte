<script lang="ts">
    let isDragging: boolean = false;

    function handleDragEnter() {
        isDragging = true;
    }

    function handleDragLeave() {
        isDragging = false;
    }

    function handleDrop(event: DragEvent) {
        event.preventDefault();
        if (!event.dataTransfer) return;

        isDragging = false;
        const files = event.dataTransfer.files;
        handleFile(files);
    }

    function handleFileSelection(
        event: Event & { currentTarget: EventTarget & HTMLInputElement }
    ) {
        const inputElement = event.target as HTMLInputElement;
        const selectedFiles = inputElement.files;

        if (selectedFiles && selectedFiles.length > 0) {
            handleFile(selectedFiles);
        }
    }

    function handleFile(files: FileList) {
        if (files.length === 0) return;

        for (let i = 0; i < files.length; i++) {
            const file = files[i];
            console.log("File:", file.name);
        }
    }

    function handleClick() {
        const fileInput = document.getElementById(
            "fileInput"
        ) as HTMLInputElement;
        fileInput.click();
    }
</script>

<main>
    <div
        on:dragenter={handleDragEnter}
        on:dragover={(event) => event.preventDefault()}
        on:dragleave={handleDragLeave}
        on:drop={(event) => handleDrop(event)}
        class:isDragging
        class="drop-zone"
        role="button"
        tabindex="0"
        on:click={handleClick}
        on:keydown={(event) => {
            if (event.key === "Enter") {
                handleClick();
            }
        }}
    >
        {#if isDragging}
            <p>Drop your file here</p>
        {:else}
            <p>Drag and drop a file here or click to browse</p>
        {/if}
    </div>

    <input
        type="file"
        id="fileInput"
        style="display: none;"
        on:change={handleFileSelection}
    />

    <p>max size: 400mb</p>
    <p>function: crypto_aead_chacha20poly1305_ietf_encrypt</p>
</main>

<style>
    .drop-zone {
        width: 99%;
        height: 80vh;
        outline: dashed 2px var(--text) !important;
        text-align: center;
        padding: 20px;
        cursor: pointer;
        margin-bottom: 1em;
    }

    .isDragging {
        color: var(--light);
        background-color: var(--background-darker);
    }
</style>
