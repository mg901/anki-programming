## [Turtle](https://www.greatfrontend.com/questions/javascript/turtle?language=js&tab=coding)

```js
const DEGREES_RIGHT_ANGLE = 90;
const HALF_CIRCLE_DEGREES = 180;
const FULL_CIRCLE_DEGREES = 360;

export default class Turtle {
  #x = 0;

  #y = 0;

  #angle = DEGREES_RIGHT_ANGLE;

  forward(distance) {
    const radians = this.#degreesToRadians(this.#angle);

    this.#x += Math.round(distance * Math.cos(radians));
    this.#y += Math.round(distance * Math.sin(radians));

    return this;
  }

  #degreesToRadians(degrees) {
    return degrees * (Math.PI / HALF_CIRCLE_DEGREES);
  }

  backward(distance) {
    return this.forward(-distance);
  }

  left() {
    this.#angle = (this.#angle + DEGREES_RIGHT_ANGLE) % FULL_CIRCLE_DEGREES;

    return this;
  }

  right() {
    this.#angle =
      (this.#angle - DEGREES_RIGHT_ANGLE + FULL_CIRCLE_DEGREES) %
      FULL_CIRCLE_DEGREES;

    return this;
  }

  position() {
    return [this.#x, this.#y];
  }
}
}
```
