<script>
  export let type = "text";
  export let value = "";
  export let margin = "";
  export let title = "";
  export let onChange;
  export let width;
  export let error = false;

  let style = "";
  if (margin) {
    style += `margin: ${margin}; `;
  }
  if (width) {
    style += `width: ${width}; `;
  }

  const handleInput = (e) => {
    let newValue = type.match(/^(number|range)$/)
      ? +e.target.value
      : e.target.value;
    onChange(newValue);
  };
</script>

<div {style}>
  <p class={`title ${error ? "error-title" : ""}`}>{title}</p>
  <input
    {type}
    {value}
    required
    on:input={handleInput}
    class={error ? "error-input" : ""}
  />
</div>

<style>
  .title {
    margin-left: 6px;
    font-weight: 300;
  }

  input {
    text-align: left;
    box-sizing: border-box;
    padding: 4px 6px 6px 6px;
    background: transparent;
    outline: none;
    color: #333;
    width: 100%;
    border-width: 0;
    border-style: hidden;
    border-image: linear-gradient(
        to right,
        var(--maincolorFaded),
        var(--maincolorFaded)
      )
      1;
    border-bottom-width: 2px;
    border-bottom-style: solid;
    transition: border-image 150ms;
    /* @media (max-width: 900px) {
      padding: 9px $paddingSmall;
    } */
  }
  input:focus,
  input:valid {
    border-image: linear-gradient(to right, var(--maincolor), var(--maincolor))
      1;
  }

  .error-input {
    background-color: var(--errorBgColor);
  }
  .error-title {
    color: var(--errorColor);
    font-weight: bold;
  }
</style>
