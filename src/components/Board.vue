
<template>
<div>
   <div class="status">{{status}}</div>
        <div class="board-row">
        <square  :value= "squares[0]"  @click.native.once= "handleClick(0)"></square>
        <!--The .native directive allows to listen for a
        native event on the root element of a component-->
        <square  :value= "squares[1]"  @click.native.once= "handleClick(1)"></square>
        <square  :value= "squares[2]"  @click.native.once= "handleClick(2)"></square>
        </div>
        <div class="board-row">
        <square  :value= "squares[3]" @click.native.once= "handleClick(3)"></square>
         <square  :value= "squares[4]"  @click.native.once= "handleClick(4)"></square>
          <square  :value= "squares[5]"  @click.native.once= "handleClick(5)"></square>
        </div>
        <div class="board-row">
          <square  :value= "squares[6]"  @click.native.once= "handleClick(6)"></square>
           <square  :value= "squares[7]"  @click.native.once= "handleClick(7)"></square>
            <square  :value= "squares[8]" @click.native.once= "handleClick(8)"></square>
        </div>
        <ul>

</ul>
</div>


</template>

<script>
import Square from './Square';

export default {
    name: 'Board',
    components: {
        Square,
    },
    data() {
        return {
            squares: Array(9).fill(null),
            xIsNext: true,
        };
    },
    computed: {
        status() {
            const winner = this.calculateWinner(this.squares);
            if (winner) {
                return `Winner: ${winner}`;
            }
            return `Next player ${this.xIsNext ? 'X' : 'O'}`;
        },
    },
    methods: {
        handleClick(i) {
            if (this.calculateWinner(this.squares) || this.squares[i]) {
                return;
            }
            const squares = this.squares.slice();
            squares[i] = this.xIsNext ? 'X' : '0';
            this.squares = squares;
            this.xIsNext = !this.xIsNext;
        },
        calculateWinner(squares) {
            const lines = [
                [0, 1, 2],
                [3, 4, 5],
                [6, 7, 8],
                [0, 3, 6],
                [1, 4, 7],
                [2, 5, 8],
                [0, 4, 8],
                [2, 4, 6],
            ];
            // eslint-disable-next-line
            for (let i = 0; i < lines.length; i++) {
                const [a, b, c] = lines[i];
                if (
                    squares[a] &&
                    squares[a] === squares[b] &&
                    squares[a] === squares[c]
                ) {
                    return squares[a];
                }
            }
            return null;
        },
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
