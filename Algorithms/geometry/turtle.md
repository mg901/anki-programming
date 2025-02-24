## [Turtle](https://www.greatfrontend.com/questions/javascript/turtle?language=js&tab=coding)

<!-- notecardId: 1740219712529 -->

```js
export default class Turtle {
  #x = 0;

  #y = 0;

  #DEGREES_RIGHT_ANGLE = 90;

  #HALF_CIRCLE_DEGREES = 180;

  #FULL_CIRCLE_DEGREES = 360;

  #angle = this.#DEGREES_RIGHT_ANGLE;

  forward(distance) {
    const radians = this.#degreesToRadians(this.#angle);

    this.#x += Math.round(distance * Math.cos(radians));
    this.#y += Math.round(distance * Math.sin(radians));

    return this;
  }

  #degreesToRadians(degrees) {
    return degrees * (Math.PI / this.#HALF_CIRCLE_DEGREES);
  }

  backward(distance) {
    return this.forward(-distance);
  }

  left() {
    this.#angle =
      (this.#angle + this.#DEGREES_RIGHT_ANGLE) % this.#FULL_CIRCLE_DEGREES;

    return this;
  }

  right() {
    this.#angle =
      (this.#angle - this.#DEGREES_RIGHT_ANGLE + this.#FULL_CIRCLE_DEGREES) %
      this.#FULL_CIRCLE_DEGREES;

    return this;
  }

  position() {
    return [this.#x, this.#y];
  }
}
```
