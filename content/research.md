---
disableComments: true
---
<style>
    #papers {
        list-style: none;
        padding: 0;
        counter-reset: item;
    }
    
    .paper {
        /* background-color: #3a3a3a; */
        border: 1px solid #676767ff;
        padding: 15px 20px;
        margin-bottom: 20px;
        border-radius: 2px;
        counter-increment: item;
        position: relative;
    }
    
    .paper:before {
        font-weight: normal;
        /* color: #e0e0e0; */
        margin-right: 10px;
        font-size: 1.2em;
    }
    
    .paper h5 {
        display: inline;
        margin: 0;
        font-size: 1.2em;
        /* color: #ffffff; */
        font-weight: normal;
    }

    .paper span {
        display: inline;
        margin: 0;
        font-size: 0.8em;
        /* color: #ffffff; */
        font-weight: normal;
    }
    
    /* .paper:hover {
        background-color: #424242;
        transition: all 0.2s ease;
    } */

    .cd-toggle {
        font-size: 0.9em;
        margin-bottom: 15px;
        display: block;
    }

    .cd-toggle {
        cursor: pointer;
        user-select: none;
    }

    .cd-icon {
        display: none;
        text-decoration: none;
        margin-left: 6px;
        vertical-align: middle;
        position: relative;
    }

    .cd-icon img {
        width: 1em;
        height: 1em;
        vertical-align: -0.15em;
    }

    body.show-cds .cd-icon {
        display: inline-block;
    }

    .cd-icon:hover img {
        transform: scale(1.15);
    }

    .cd-icon[data-tooltip]:before {
        content: attr(data-tooltip);
        position: absolute;
        bottom: 130%;
        left: 50%;
        transform: translateX(-50%);
        background: #222;
        color: #eee;
        padding: 4px 8px;
        border-radius: 4px;
        font-size: 0.75em;
        white-space: nowrap;
        opacity: 0;
        pointer-events: none;
        transition: opacity 0.15s ease;
        z-index: 10;
    }

    .cd-icon[data-tooltip]:after {
        content: "";
        position: absolute;
        bottom: 115%;
        left: 50%;
        transform: translateX(-50%);
        border: 5px solid transparent;
        border-top-color: #222;
        opacity: 0;
        pointer-events: none;
        transition: opacity 0.15s ease;
        z-index: 10;
    }

    .cd-icon[data-tooltip]:hover:before,
    .cd-icon[data-tooltip]:hover:after {
        opacity: 1;
    }
</style>

<h1>Selected papers</h1>
<p>See my <a href="https://scholar.google.com/citations?user=4EobJQIAAAAJ&hl=en&oi=sra">Google Scholar</a> for a full list of publications.</p>

<ol id="papers">
    <li class="paper">
    <a href="https://ocr.baulab.info/"><h5>Using OCR Heads to Verbalize Image Semantics</h5></a><a class="cd-icon" href="https://www.youtube.com/watch?v=2FUiZYrPZWk" target="_blank" rel="noopener" data-tooltip="Summer 2026"><img src="/hm_sprite.png" alt="CD"></a><br>
    <span><b>Sheridan Feucht</b>, Benno Krojer, Sarah Wang, Henry Abrahamsen, Byron Wallace, David Bau</span><br>
    <span>Preprint, 2026.</span>
    </li>
    <li class="paper">
    <a href="https://www.goodfire.ai/research/a-geometric-calculator#"><h5>Arithmetic in the Wild: Llama uses Base-10 Addition to Reason About Cyclic Concepts</h5></a><a class="cd-icon" href="https://www.youtube.com/watch?v=PFW2uSCZ0uE" target="_blank" rel="noopener" data-tooltip="This paper has lots of these objects..."><img src="/hm_sprite.png" alt="CD"></a><br>
    <span><b>Sheridan Feucht*</b>, Tal Haklay*, Usha Bhalla, Daniel Wurgaft, Can Rager, Raphaël Sarfati, Jack Merullo, Thomas McGrath, Owen Lewis, Ekdeep Singh Lubana*, Thomas Fel*, Atticus Geiger*</span><br>
    <span>Third Conference on Language Modeling (COLM), 2026.</span>
    </li>
    <li class="paper">
    <a href="https://dualroute.baulab.info/"><h5>The Dual-Route Model of Induction</h5></a><a class="cd-icon" href="https://www.youtube.com/watch?v=WMDWPH4oKwo" target="_blank" rel="noopener" data-tooltip="Type Slowly for token induction..."><img src="/hm_water.png" alt="CD"></a><a class="cd-icon" href="https://www.youtube.com/watch?v=K14qg9E9SoE" target="_blank" rel="noopener" data-tooltip="...but Slowly Typed for concept induction"><img src="/hm_fighting.png" alt="CD"></a><br>
    <span><b>Sheridan Feucht</b>, Eric Todd, Byron Wallace, David Bau</span><br>
    <span>Second Conference on Language Modeling (COLM), 2025.</span>
    </li>
    <li class="paper">
        <a href="https://footprints.baulab.info/"><h5> Token Erasure as a Footprint of Implicit Vocabulary Items in LLMs</h5></a><a class="cd-icon" href="https://www.youtube.com/watch?v=O-rrt8IYhe0" target="_blank" rel="noopener" data-tooltip="Lexical footprints..."><img src="/hm_sprite.png" alt="CD"></a><br>
        <span><b>Sheridan Feucht</b>, David Atkinson, Byron Wallace, David Bau</span><br>
        <span>Empirical Methods in Natural Language Processing (EMNLP), 2024.</span>
    </li>
</ol>

<p class="cd-toggle" id="cd-toggle-trigger">
    <i>click me to see a hand-picked track for each paper 🎧</i>
</p>

<h1>Other Works</h1>
<ol id="papers">
    <li class="paper">
        <a href="https://arithmetic.baulab.info/"><h5>Vector Arithmetic in Concept and Token Subspaces</h5></a><br>
        <span><b>Sheridan Feucht</b>, Byron Wallace, David Bau</span><br>
        <span>Mechanistic Interpretability Workshop at NeurIPS, 2025.</span>
    </li>
    <li class="paper">
        <a href="https://openreview.net/pdf?id=MT9zaJoHjp"><h5>Does FLUX Know What It's Writing?</h5></a><a class="cd-icon" href="https://www.youtube.com/watch?v=7qsHVvKvr2I" target="_blank" rel="noopener" data-tooltip="Flux is pretty rad."><img src="/hm_sprite.png" alt="CD"></a><br>
        <span>Adrian Chang*, <b>Sheridan Feucht*</b>, Byron Wallace, David Bau</span><br>
        <span>Mechanistic Interpretability Workshop at NeurIPS, 2025.</span>
    </li>
    <li class="paper">
        <a href="https://arxiv.org/pdf/2511.05743"><h5>In-Context Learning Without Copying</h5></a><br>
        <span>Kerem Sahin, <b>Sheridan Feucht</b>, Adam Belfki, Jannik Brinkmann, Aaron Mueller, David Bau, Chris Wendler</span><br>
        <span>Preprint (November 2025).</span>
    </li>
    <li class="paper">
        <a href="https://elm.baulab.info/"><h5>Erasing Conceptual Knowledge from Language Models</h5></a><br>
        <span>Rohit Gandikota, <b>Sheridan Feucht</b>, Samuel Marks, David Bau</span><br>
        <span>Conference on Neural Information Processing Systems (NeurIPS), 2025.</span>
    </li>
    <li class="paper">
        <a href="https://arxiv.org/pdf/2310.09612"><h5>Deep Neural Networks Can Learn Generalizable Same-Different Visual Relations</h5></a><br>
        <span>Alexa R. Tartaglini*, <b>Sheridan Feucht*</b>, Michael A. Lepori, Wai Keen Vong, Charles Lovering, Brenden M. Lake, Ellie Pavlick</span><br>
        <span>Conference on Cognitive Computational Neuroscience, 2025.</span>
    </li>
</ol>

<script>
(function () {
    var trigger = document.getElementById('cd-toggle-trigger');
    trigger.addEventListener('click', function () {
        document.body.classList.toggle('show-cds');
    });
})();
</script>

