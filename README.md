interface SimpleProps {
  width?: number;
  height: number;
  theme: 'light' | 'dark';
  message: string;
}

const simpleSharedStyles = /*css*/ `
  :root {
    --color-text-light: #1a1a1a;
    --color-text-dark: #f0f0f0;
    --typing-speed: 50ms;
  }
  [data-theme="light"] {
    color: var(--color-text-light);
    background: #fff;
  }
  [data-theme="dark"] {
    color: var(--color-text-dark);
    background: #121212;
  }
  .wrapper {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 20px;
    display: flex;
    align-items: center;
    height: 100%;
    padding: 1rem;
    white-space: nowrap;
    overflow: hidden;
    border-radius: 8px;
  }
  .typing span {
    opacity: 0;
    animation: typeIn 0.1s forwards;
    animation-fill-mode: forwards;
  }
  .cursor {
    width: 0.6em;
    height: 1.2em;
    background-color: currentColor;
    margin-left: 4px;
    animation: blink 1s step-end infinite;
  }
  @keyframes typeIn {
    to {
      opacity: 1;
    }
  }
  @keyframes blink {
    0%, 100% {
      opacity: 1;
    }
    50% {
      opacity: 0;
    }
  }
`;

export const simpleTypingSVG = (props: SimpleProps) => {
  const styles = /*css*/ `
    ${simpleSharedStyles}
  `;

  const chars = [...props.message].map(
    (char, i) => `<span style="animation-delay:${i * 50}ms">${char}</span>`
  ).join('');

  const attributes = {
    width: props.width ? props.width.toString() : '100%',
    height: props.height.toString(),
    'data-theme': props.theme,
  };

  return `
  <svg xmlns="http://www.w3.org/2000/svg" ${attr(attributes)} fill="none">
    <foreignObject width="100%" height="100%">
      <div xmlns="http://www.w3.org/1999/xhtml" class="wrapper" data-theme="${props.theme}">
        <style>${styles}</style>
        <div class="typing">${chars}<span class="cursor"></span></div>
      </div>
    </foreignObject>
  </svg>
  `;
};
