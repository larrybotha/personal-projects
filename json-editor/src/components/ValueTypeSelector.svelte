<script>
  import Button from './Button.svelte';
  import * as props from './Button.svelte';
  import Selector from './Selector.svelte';

  export let service;

  let buttonProps = [
    {
      text: 'x',
      handler: () => handleClick('SELECT_PRIMITIVE'),
    },
    {
      text: '[ ]',
      handler: () => handleClick('SELECT_ARRAY'),
    },
    {
      text: '{ }',
      handler: () => handleClick('SELECT_OBJECT'),
    },
  ];

  const handleClick = eventType => service.send(eventType);

  $: getButtonContent = () => {
    switch (true) {
      case $service.matches('primitive'):
        return 'x';
      case $service.matches('object'):
        return '{ }';
      case $service.matches('array'):
        return '[ ]';
      default:
        return;
    }
  };
</script>

<Selector buttonContent={getButtonContent()} let:item items={buttonProps}>
  <Button on:click={item.handler}>{item.text}</Button>
</Selector>
