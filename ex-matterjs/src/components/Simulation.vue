<script>
import Matter from "matter-js";

export default {
  name: "Simulation",

  data() {
    return {
      bounceCount: 0,
      engine: null,
      render: null,
      squareA: null,
      squareB: null,
      isSimulationRunning: false,
    };
  },

  methods: {
    startSimulation() {
      if (!this.isSimulationRunning) {
        // Reset the bounce count
        this.bounceCount = 0;
        this.isSimulationRunning = true;

        // Launch square B with an initial velocity
        this.launchSquareB();

        // Start updating the simulation
        this.updateSimulation();
      }
    },

    resetSimulation() {
      // Reset the positions of squareA and squareB
      Matter.Body.setPosition(this.squareA, { x: 500, y: 100 });
      Matter.Body.setPosition(this.squareB, { x: 300, y: 100 });

      // Reset the bounce count
      this.bounceCount = 0;
      this.isSimulationRunning = false;
    },

    launchSquareB() {
      // Set an initial velocity to square B
      const initialVelocityX = -20; // Adjust this velocity as needed
      Matter.Body.setVelocity(this.squareA, { x: initialVelocityX, y: 0 });
    },

    updateSimulation() {
      if (this.isSimulationRunning) {
        // Request the next animation frame
        requestAnimationFrame(this.updateSimulation);
      }
    },
  },

  mounted() {
    // Create a Matter.js engine
    this.engine = Matter.Engine.create();

    // Create a Matter.js renderer
    this.render = Matter.Render.create({
      element: this.$refs.matterCanvas,
      engine: this.engine,
      options: {
        width: 1400,
        height: 1000,
        pixelRatio: 1,
        background: "#161616",
        wireframeBackground: "#161616",
        hasBounds: true,
        enabled: true,
        wireframes: false, // Disable wireframes to show filled bodies
        showSleeping: true,
        showDebug: false, // Hide debugging info
        showBroadphase: false,
        showBounds: false,
        showVelocity: false,
        showCollisions: false,
        showSeparations: false,
        showAxes: false,
        showPositions: false,
        showAngleIndicator: false,
        showIds: false,
        showShadows: false,
        showVertexNumbers: false,
        showConvexHulls: false,
        showInternalEdges: false,
        showMousePosition: false,
      },
    });
    // Create some bodies (shapes) using Matter.js
    const wallLeft = Matter.Bodies.rectangle(0, 500, 20, 1000, {
      isStatic: true,
    });
    const wallRight = Matter.Bodies.rectangle(1400, 500, 20, 1000, {
      isStatic: true,
    });

    const ground = Matter.Bodies.rectangle(700, 1000, 1400, 40, {
      isStatic: true,
      friction: 0,
    });

    this.squareA = Matter.Bodies.rectangle(500, 100, 100, 100, {
      friction: 0,
    });
    this.squareB = Matter.Bodies.rectangle(300, 100, 50, 50, {
      friction: 0,
    });

    // Check if the bodies were created successfully and are not null
    if (this.squareA && this.squareB) {

      Matter.World.add(this.engine.world, [
        wallLeft,
        wallRight,
        ground,
        this.squareA,
        this.squareB,
      ]);
    }

    // Start the engine and renderer
    Matter.Runner.run(this.engine);
    Matter.Render.run(this.render);
  },
};
</script>

<template>
  <div>
    <div ref="matterCanvas"></div>
    <h2>Results</h2>
    <h3>Bounce Counts: {{ bounceCount }}</h3>
    <div>
      <button @click="startSimulation" class="btn btn-primary">
        Start Simulation
      </button>
      <button @click="resetSimulation" class="btn btn-warning">
        Reset Simulation
      </button>
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
