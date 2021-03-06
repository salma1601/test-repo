

.. _sphx_glr_auto_examples_plot_heroes_realign.py:


================
Realignment demo
================

This example compares standard realignement to realignement with tagging
correction.


../examples/plot_heroes_realign.py is not compiling:




.. code-block:: python

    # Create a memory context
    from nipype.caching import Memory
    mem = Memory('/tmp')

    # Give the path to the 4D ASL image
    raw_asl_file = '/tmp/func.nii'

    # Realign with and without tagging correction
    from procasl import preprocessing
    import numpy as np
    realign = mem.cache(preprocessing.Realign)
    x_translation = {}
    for correct_tagging in [True, False]:
        out_realign = realign(in_file=raw_asl_file,
                              correct_tagging=correct_tagging)
        x_translation[correct_tagging] = np.loadtxt(
            out_realign.outputs.realignment_parameters)[:, 2]

    # Plot x-translation parameters with and without tagging correction
    import matplotlib.pylab as plt
    plt.figure(figsize=(10, 5))
    for correct_tagging, label, color in zip([True, False],
                                             ['corrected', 'uncorrected'], 'rb'):
        plt.plot(x_translation[correct_tagging], label=label, color=color)
    plt.ylabel('translation in x [mm]')
    plt.legend()
    figure = plt.figure(figsize=(10, 5))
    plt.plot(x_translation[True] - x_translation[False], color='g')
    plt.ylabel('difference [mm]')
    plt.xlabel('frame')
    figure.suptitle('Impact of tagging correction')
    plt.show()

**Total running time of the script:**
(0 minutes 0.000 seconds)



**Download Python source code:** :download:`plot_heroes_realign.py <plot_heroes_realign.py>`
