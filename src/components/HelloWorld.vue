<template>
  <v-container>
    <h1>TWO + TWO = FOUR</h1>
    <v-row>
      <v-col cols="12" sm="6">
        <v-text-field
          v-model="T"
          label="Possible values for : T, F"
          outlined
          shaped
          readonly
        ></v-text-field>
      </v-col>

      <v-col cols="12" sm="6">
        <v-text-field
          v-model="W"
          label="Possible values for : W, O, U, R"
          outlined
          shaped
          readonly
        ></v-text-field>
      </v-col>
      <v-col cols="12" sm="6">
        <v-text-field
          v-model="C1"
          label="C1"
          outlined
          shaped
          readonly
        ></v-text-field>
      </v-col>
      <v-col cols="12" sm="6">
        <v-text-field
          v-model="C2"
          label="C2"
          outlined
          shaped
          readonly
        ></v-text-field>
      </v-col>
      <v-col cols="12" sm="12">
        <v-textarea
          name="contraints"
          label="Contraints"
          v-model="contraints"
          rows="1"
          outlined
          readonly
        ></v-textarea>
      </v-col>
      <v-col cols="12" sm="12">
        <v-textarea
          name="solutions"
          label="Solutions"
          v-model="solutions"
          outlined
          readonly
        ></v-textarea>
      </v-col>
      <v-col cols="12" sm="12">
        <v-btn rounded color="success" small @click="computeSolution()">
          See possible solutions
          <v-icon right dark> mdi-plus </v-icon>
        </v-btn>
      </v-col>
    </v-row>
    <h1>MAGIC SQUARE</h1>
    <v-row>
      <v-col cols="12" sm="12">
        <v-textarea
          name="Magic"
          label="Magic Square Solutions"
          v-model="magicSolutions"
          outlined
          readonly
        ></v-textarea>
      </v-col>

      <v-col cols="12" sm="12">
        <v-btn rounded color="success" small @click="magicSolve()">
          See possible solutions
          <v-icon right dark> mdi-plus </v-icon>
        </v-btn>
      </v-col>
    </v-row>
    <h1>N-QUEENS</h1>
    <v-row>
      <v-col cols="12" sm="12">
        <v-textarea
          name="Queens"
          label="N-Queens Solutions"
          v-model="queensSolutions"
          outlined
          readonly
        ></v-textarea>
      </v-col>

      <v-col cols="12" sm="12">
        <v-btn rounded color="success" small @click="magicSolve()">
          See possible solutions
          <v-icon right dark> mdi-plus </v-icon>
        </v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script >
import process from "process";
export default {
  components: {},
  data: () => ({
    T: [1, 2, 3, 4, 5, 6, 7, 8, 9],
    W: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
    O: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
    F: [1, 2, 3, 4, 5, 6, 7, 8, 9],
    U: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
    R: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
    C1: [0, 1],
    C2: [0, 1, 2],
    iterations: 0,
    contraints:
      "- All letters have different values, addition works as intended, leading digits (letters) aren't zero (T, F).                                                                                                                                    O + O = R + 10 * C_1 |||||| W + W + C_1 = U + 10*C_10 |||||| T + T + C_10 = O + 10*F ",
    solutions: "Solutions according to this order : T, W, O, F, U, R : (I hope that you have a strong computer ! because it might take many minutes :(  )",
    magicSolutions: "Here are the solutions : (I hope that you have a strong computer ! because it might take many minutes :(  )) ",
    queensSolutions: "Here are the solutions : (I hope that you have a strong computer ! because it might take many minutes :(  )) ",
  }),

  computed: {},

  methods: {
    magicSolve() {
      /* eslint-disable no-console */
      console.log("ça commence !");
      /* eslint-disable no-console */
      for (let c11 = 1; c11 <= 9; c11++) {
        for (let c12 = 1; c12 <= 9; c12++) {
          for (let c13 = 1; c13 <= 9; c13++) {
            for (let c21 = 1; c21 <= 9; c21++) {
              for (let c22 = 1; c22 <= 9; c22++) {
                for (let c23 = 1; c23 <= 9; c23++) {
                  for (let c31 = 1; c31 <= 9; c31++) {
                    for (let c32 = 1; c32 <= 9; c32++) {
                      for (let c33 = 1; c33 <= 9; c33++) {
                        if (
                          this.allDifferent([
                            c11,
                            c12,
                            c13,
                            c21,
                            c22,
                            c23,
                            c31,
                            c32,
                            c33,
                          ])
                        ) {
                          if (
                            this.magicConstraint([
                              c11,
                              c12,
                              c13,
                              c21,
                              c22,
                              c23,
                              c31,
                              c32,
                              c33,
                            ])
                          ) {
                            this.magicSolutions =
                              this.magicSolutions +
                              [c11, c12, c13, c21, c22, c23, c31, c32, c33] +
                              ", ";
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          }
        }
      }
    },
    magicConstraint(values) {
      /* eslint-disable no-console */
      console.log("TEEEEEEEEST");
      console.log(values + "values");
      /* eslint-disable no-console */
      if (values[0] + values[1] + values[2] === 15) {
        if (values[3] + values[4] + values[5] === 15) {
          if (values[6] + values[7] + values[8] === 15) {
            if (values[0] + values[3] + values[6] === 15) {
              if (values[1] + values[4] + values[7] === 15) {
                if (values[2] + values[5] + values[8] === 15) {
                  if (values[0] + values[4] + values[8] === 15) {
                    if (values[2] + values[4] + values[6] === 15) {
                      return true;
                    } else {
                      return false;
                    }
                  } else {
                    return false;
                  }
                } else {
                  return false;
                }
              } else {
                return false;
              }
            } else {
              return false;
            }
          } else {
            return false;
          }
        } else {
          return false;
        }
      } else {
        return false;
      }
    },
    computeSolution() {
      for (let t = 1; t <= 9; t++) {
        for (let w = 0; w <= 9; w++) {
          for (let o = 0; o <= 9; o++) {
            for (let f = 1; f <= 9; f++) {
              for (let u = 0; u <= 9; u++) {
                for (let r = 0; r <= 9; r++) {
                  for (let c1 = 0; c1 <= 1; c1++) {
                    for (let c2 = 0; c2 <= 2; c2++) {
                      if (this.allDifferent([t, w, o, f, u, r])) {
                        if (
                          this.computeConstraint([o, r, c1, w, u, c2, t, f])
                        ) {
                          this.solutions =
                            this.solutions + [t, w, o, f, u, r] + ", ";
                          return [t, w, o, f, u, r];
                        }
                      }
                    }
                  }
                }
              }
            }
          }
        }
      }
    },
    allDifferent(values) {
      let different = true;
      let unique = [...new Set(values)];
      if (unique.length != values.length) {
        different = false;
      }
      /* eslint-disable no-console */
      console.log("All different : " + different);
      /* eslint-disable no-console */
      return different;
    },
    computeConstraint(values) {
      //[o,r,c1,w,u,c2,t,f]
      //[0,1, 2,3,4, 5,6,7]
      if (values[0] + values[0] == values[1] + 10 * values[2]) {
        if (values[3] + values[3] + values[2] == values[4] + 10 * values[5]) {
          if (values[6] + values[6] + values[5] == values[0] + 10 * values[7]) {
            return true;
          } else {
            return false;
          }
        } else {
          return false;
        }
      } else {
        return false;
      }
    },
    nqueens() {
      this.print_board(this.place_next_queen(28, 28));
      console.log("\n iterations: ", this.iterations);
    },
    print_board(columns) {
      var n = columns.length,
        row = 0,
        col = 0;
      while (row < n) {
        while (col < n) {
          process.stdout.write(columns[row] === col ? "Q " : "# ");
          col++;
        }

        process.stdout.write("\n");
        col = 0;
        row++;
      }
    },
    has_conflict(columns) {
      var len = columns.length,
        last = columns[len - 1],
        previous = len - 2;

      while (previous >= 0) {
        if (columns[previous] === last) return true;
        if (last - (len - 1) === columns[previous] - previous) return true;
        if (last + (len - 1) === columns[previous] + previous) return true;
        previous--;
      }

      return false;
    },
    place_next_queen(total, queens, columns) {
      if (queens === 0) return columns;
      columns = columns || [];

      for (var column = 0; column < total; column++) {
        columns.push(column);
        this.iterations++;
        if (
          !this.has_conflict(columns) &&
          this.place_next_queen(total, queens - 1, columns)
        ) {
          return columns;
        }
        columns.pop(column);
      }

      return null;
    },
  },
};
</script>

