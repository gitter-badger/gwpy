############################################################################
The spectrum (:class:`gwpy.spectrum.Spectrum <gwpy.spectrum.core.Spectrum>`)
############################################################################

.. currentmodule:: gwpy.spectrum.core

.. code-block:: python

   >>> from gwpy.spectrum import Spectrum

While gravitational-wave detectors are time-domain instruments, their sensitivity is frequency dependent and so is often measured as a power-spectral-density over the range of interesting gravitational-wave frequencies (~10-10,000 Hz).
Additionally, the auxiliary `channels <../detector/channel>`_ used to sense and control instrumental operations each have their own frequency-domain characteristics, contributing to the overall sensivitity spectrum.

The :class:`Spectrum` object is used to represent any frequency series, including the power-spectral (and amplitude-spectral) density series describing instrument performance.

Analogously to the :class:`~gwpy.timeseries.core.TimeSeries`, a new `Spectrum` can be generated from any data sequence along with the minimal :attr:`~Spectrum.f0` and :attr:`~Spectrum.df` metadata::

    >>> from gwpy.spectrum import Spectrum
    >>> spec = Spectrum([1,2,3,4,5,6,7,8,9,10], f0=0, df=1)
    >>> print(spec)
    Spectrum([ 1  2  3  4  5  6  7  8  9 10],
             name: None,
             unit: None,
             epoch: None,
             channel: None,
             f0: 0 Hz,
             df: 1 Hz,
             logf: False)

The full set of metadata that can be provided is as follows:

.. autosummary::

   ~Spectrum.name
   ~Spectrum.unit
   ~Spectrum.epoch
   ~Spectrum.f0
   ~Spectrum.df

===========================================================================
Generating a `Spectrum` from a :class:`~gwpy.timeseries.core.TimeSeries`
===========================================================================

.. currentmodule:: gwpy.timeseries.core

The frequency-spectrum of a :class:`TimeSeries` can be calculated using either of the following methods:

.. autosummary::
   :nosignatures:

   TimeSeries.psd
   TimeSeries.asd

In this example we expand the :ref:`previous example <plotting-a-timeseries>`, by calculating the amplitude-spectral density of the gravitational-wave strain data from LHO:

.. literalinclude:: spectrum_plot.py
   :lines: 1-3

where the result is an average spectrum calculated using the `Welch method <https://en.wikipedia.org/wiki/Welch_method>`_.

=====================
Plotting a `Spectrum`
=====================

.. currentmodule:: gwpy.spectrum.core

Similary to the :class:`~gwpy.timeseries.core.TimeSeries`, the `Spectrum` object comes with its own :meth:`~Spectrum.plot` method, which will quickly construct a :class:`~gwpy.plotter.timeseries.SpectrumPlot`:

.. plot:: spectrum/spectrum_plot.py
   :include-source: