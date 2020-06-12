## Flavours of Retention

Cut and paste the wavedrom code in to https://wavedrom.com/editor.html

### 1 pin retention on power-up, ignore reset/clock

```wavedrom
{signal: [{name: 'CLK',       wave: 'P...x.....0P...', period: 2},  
          {name: 'D',         wave: 'x3.4.5.x.............3.4.5.6.7', data: 'D1 D2 D3 D4 D5 D6 D7 D8 D9 D10 D11 D12'},
          {name: 'Q',         wave: 'x.3.4.5....z.....5....3.4.5.6.', data: 'D1 D2 D3 D3 D4 D5 D6 D7'},  
          {name: 'RESET',     wave: 'x.............................'},  
          {name: 'RETN',      wave: '1......0.............1........', node: '.......a.............d........'},  
          {name: 'PWR',       wave: '1..........0.....1............', node: '...........b.....c............'},   
          {},  
          {                   node: '.......A...B.....C...D........'},   
         ],  
         edge: [
          'a--A',
          'b--B',
          'c--C',
          'd--D',
          'A<-|->B restore',
          'B<-|->C retention period',
          'C<-|->D restore'], 
 foot:{   tick:0,   text:'1 pin, restore on power-up, ignore reset/clock', }, 
 config: { skin: "narrow"}}
```
 
### 1 pin, restore on power-up, obey reset
 
```wavedrom
{signal: [{name: 'CLK',       wave: 'P...x.....0P...', period: 2},  
          {name: 'D',         wave: 'x3.4.5.x.............3.4.5.6.7', data: 'D1 D2 D3 D4 D5 D6 D7 D8 D9 D10 D11 D12'},
          {name: 'Q',         wave: 'x.3.4.5....z.....0....3.4.5.6.', data: 'D1 D2 D3 D3 D4 D5 D6 D7'},  
          {name: 'RESET',     wave: '0.............1.........0.....'},  
          {name: 'RETN',      wave: '1......0.............1........', node: '.......a.............d........'},  
          {name: 'PWR',       wave: '1..........0.....1............', node: '...........b.....c............'},   
          {},  
          {                   node: '.......A...B.....C...D........'},   
         ],  
         edge: [
          'a--A',
          'b--B',
          'c--C',
          'd--D',
          'A<-|->B restore',
          'B<-|->C retention period',
          'C<-|->D restore'], 
 foot:{   tick:0,   text:'1 pin, restore on power-up, ignore reset/clock', }, 
 config: { skin: "narrow"}}
```

### 1 pin, restore on power-up, obey reset when not in retention

```wavedrom
{signal: [{name: 'CLK',       wave: 'P...x.....0P...', period: 2},  
          {name: 'D',         wave: 'x3.4.5.x.............3.4.5.6.7', data: 'D1 D2 D3 D4 D5 D6 D7 D8 D9 D10 D11 D12'},
          {name: 'Q',         wave: 'x.3.4.5x...z.....x...03.4.5.6.', data: 'D1 D2 D3 D3 D4 D5 D6 D7'},  
          {name: 'RESET',     wave: '0.............1.........0.....'},  
          {name: 'RETN',      wave: '1......0.............1........', node: '.......a.............d........'},  
          {name: 'PWR',       wave: '1..........0.....1............', node: '...........b.....c............'},   
          {},  
          {                   node: '.......A...B.....C...D........'},   
         ],  
         edge: [
          'a--A',
          'b--B',
          'c--C',
          'd--D',
          'A<-|->B restore',
          'B<-|->C retention period',
          'C<-|->D restore'], 
 foot:{   tick:0,   text:'1 pin, restore on power-up, obey reset when not in retention', }, 
 config: { skin: "narrow"}}

```

### 1-pin, restore on power-up, ignore reset, clock must be low
 ```wavedrom
{signal: [{name: 'CLK',       wave: 'P....lx..0.P...', period: 2},  
          {name: 'D',         wave: 'x3.4.5.x.............3.4.5.6.7', data: 'D1 D2 D3 D4 D5 D6 D7 D8 D9 D10 D11 D12'},
          {name: 'Q',         wave: 'x.3.4.5x...z.....5...03.4.5.6.', data: 'D1 D2 D3 D3 D4 D5 D6 D7'},  
          {name: 'RESET',     wave: '0......x......1.........0.....'},  
          {name: 'RETN',      wave: '1......0.............1........', node: '.......a.............d........'},  
          {name: 'PWR',       wave: '1..........0.....1............', node: '...........b.....c............'},   
          {},  
          {                   node: '.......A...B.....C...D........'},   
         ],  
         edge: [
          'a--A',
          'b--B',
          'c--C',
          'd--D',
          'A<-|->B restore',
          'B<-|->C retention period',
          'C<-|->D restore'], 
 foot:{   tick:0,   text:'1-pin, restore on power-up, ignore reset, clock must be low', }, 
 config: { skin: "narrow"}}
```

### 1-pin, restore on power-up, obey set, reset sticky
```wavedrom
{signal: [
  {name: 'CLK',    wave: 'P...x...0P...', period: 2},
  {name: 'D',      wave: 'x3.4.5.x.........3.4.5.6.7', data: 'D1 D2 D3 D4 D5 D6 D7 D8 D9 D10 D11 D12'},
  {name: 'Q',      wave: 'x.3.4.5..z.....0..3.4.5.6.', data: 'D1 D2 D3 D4 D5 D6 D7'},
  {name: 'RESET',  wave: '0.............1.0.........'},
  {name: 'RETN',   wave: '1......0.........1........', node: '.......a.........d........'},
  {name: 'PWR',    wave: '1........0.....1..........', node: '.........b.....c..........'}, 
  ],
  edge: [
    'a~b restore period',
    'b~c retention period',
    'c~d restore period'
  ],
 foot:{
   tick:0,
   text:'1-pin, restore on power-up, obey set, reset sticky',
 },
 config: { skin: "narrow"}
}
```

### 1-pin, restore on power-up, obey reset, reset not sticky, clock must be low during restore
```
{signal: [{name: 'CLK',       wave: 'P....lx..0.P...', period: 2},  
          {name: 'D',         wave: 'x3.4.5.x.............3.4.5.6.7', data: 'D1 D2 D3 D4 D5 D6 D7 D8 D9 D10 D11 D12'},
          {name: 'Q',         wave: 'x.3.4.5x...z.....0..6.3.4.5.6.', data: 'D1 D2 D3 D3 D4 D5 D6 D7'},  
          {name: 'RESET',     wave: '0...............1...0.........'},  
          {name: 'RETN',      wave: '1......0.............1........', node: '.......a.............d........'},  
          {name: 'PWR',       wave: '1..........0.....1............', node: '...........b.....c............'},   
          {},  
          {                   node: '.......A...B.....C...D........'},   
         ],  
         edge: [
          'a--A',
          'b--B',
          'c--C',
          'd--D',
          'A<-|->B restore',
          'B<-|->C retention period',
          'C<-|->D restore'], 
 foot:{   tick:0,   text:'1-pin, restore on power-up, obey set, reset sticky', }, 
 config: { skin: "narrow"}}

```


